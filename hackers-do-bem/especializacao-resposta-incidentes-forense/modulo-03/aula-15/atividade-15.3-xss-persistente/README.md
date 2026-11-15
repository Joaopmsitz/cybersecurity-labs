# Activity 15.3 — Investigating Stored Cross-Site Scripting (XSS)

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 15  
> **Environment:** DVWA — forenseLinux and forenseWin VMs  
> **Status:** Completed

## 1. Objective

Investigate a stored Cross-Site Scripting (XSS) vulnerability in DVWA and identify the evidence persisted in the application's database.

The exercise uses the **XSS (Stored)** module.

Unlike reflected XSS, the supplied content is stored by the application and later included in pages displayed to other users.

The activity demonstrates how a malicious script can remain in a database and execute again whenever the affected page is rendered.

The investigation examines:

- The stored message in the DVWA guestbook.
- The application's database configuration.
- The MariaDB database and relevant table.
- The relationship between stored script content and subsequent application access.
- The HTTP activity recorded by Apache.

## 2. Environment

| Item | Details |
|---|---|
| Application | DVWA |
| Web Server | `forenseLinux` |
| Server IP | `192.168.98.10` |
| Attacker Workstation | `forenseWin` |
| Attacker IP | `192.168.98.30` |
| Application Module | XSS (Stored) |
| Security Level | Low |
| Database Management System | MariaDB |
| Database Name | `dvwa` |
| Database Account | `dvwa` |
| Database Server | `127.0.0.1` |
| Database Port | `3306` |
| Database Configuration | `/var/www/html/dvwa/config/config.inc.php` |
| Database Table | `guestbook` |
| Local HTTP Server Port | `8080` |

The exercise takes place in the same isolated DVWA environment used in the previous activities.

## 3. Technical Concepts

### Stored XSS

Stored XSS occurs when untrusted input is saved by an application and later rendered in a browser without appropriate output encoding or sanitization.

Common locations where stored XSS may occur include:

- Comment fields.
- Guestbooks.
- Discussion posts.
- User profile fields.
- Stored messages.
- Application records displayed to other users.

The key characteristic is persistence: the malicious content remains in the application and can affect users who access the affected content later.

### Reflected XSS Versus Stored XSS

| Characteristic | Reflected XSS | Stored XSS |
|---|---|---|
| Payload location | Usually a request parameter | Stored by the application |
| Persistence | Not normally persisted | Persisted |
| Delivery | Request and response | Later rendering of stored content |
| Victims | Usually users who open a crafted request | Users who access the affected content |
| Investigation | Request logs and application responses | Database records and access logs |

### Database Persistence

DVWA uses a database to store the guestbook entries.

The application configuration file identifies the database connection parameters.

The guestbook table contains the saved comments and associated names.

Examining the database can therefore reveal the content that was stored by the application.

### Apache Access Logs and Stored XSS

In a stored XSS scenario, the script content may not appear in the URL of the victim's later request.

The access log may therefore show only a generic page request.

The database record becomes an important source of evidence because it preserves the content that was stored and subsequently rendered.

### Session and Browser Information

The laboratory demonstrates how script execution in a browser can expose session information.

Session cookies should be protected with appropriate attributes, including `HttpOnly`, `Secure`, and `SameSite` where applicable.

These attributes reduce some attack impacts but do not replace proper output encoding and sanitization.

## 4. Procedure

### Step 1 — Open the Stored XSS Module

The DVWA application was opened on the Windows workstation:

```text
http://192.168.98.10/dvwa
```

The **XSS (Stored)** module was selected.

The application presented a form containing:

- Name.
- Message.

The submitted information was stored and displayed as a guestbook entry.

### Step 2 — Verify the Stored XSS Behavior

The activity used the following test information:

```text
Name: test
Message: <script>alert(document.cookie);</script>
```

After submission, the application displayed the stored entry.

The browser executed the JavaScript and displayed an alert.

This demonstrated that the application was storing untrusted script content and later rendering it as executable code.

### Step 3 — Start the Local HTTP Server

A local HTTP server was started on the Windows workstation:

```cmd
python -m http.server 8080
```

The server output was:

```text
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
```

The server was used by the course to observe requests associated with the stored script demonstration.

### Step 4 — Examine the Message Length Restriction

The course identified a client-side restriction in the message field.

The field initially limited input to 50 characters.

The browser developer tools were opened with:

```text
F12
```

The Message field was inspected.

Its HTML `maxlength` attribute was changed from:

```text
50
```

to:

```text
1000
```

This modified the browser-side input limit for the laboratory demonstration.

A client-side HTML restriction should not be treated as a security control because it can be changed by the user.

The server must independently validate input length and content.

### Step 5 — Observe the Stored Script Activity

The activity demonstrated the storage of a script intended to generate requests to the controlled collection server.

The exact cookie-collection JavaScript is not reproduced in this public README.

The laboratory output showed a request reaching the local HTTP server:

```text
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
192.168.98.30 - - [09/Jul/2023 01:53:43] "GET /?=[REDACTED_SESSION_DATA] HTTP/1.1" 200 -
```

The session data is redacted.

The result demonstrated that the stored content could cause browser requests when the page was accessed.

### Step 6 — Examine the Application Database Configuration

The investigation returned to the Linux server hosting DVWA.

A root shell was opened:

```bash
sudo su
```

The database configuration file was examined:

```bash
cat /var/www/html/dvwa/config/config.inc.php
```

The course material includes the following configuration excerpt:

```php
$DBMS = 'MySQL';

$_DVWA[ 'db_server' ] = getenv('DB_SERVER') ?: '127.0.0.1';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ] = 'dvwa';
$_DVWA[ 'db_password' ] = '[REDACTED]';
$_DVWA[ 'db_port'] = '3306';
```

The database password is redacted because configuration secrets should not be included in public repository documentation.

The relevant connection information is:

| Setting | Value |
|---|---|
| DBMS | MySQL-compatible MariaDB |
| Database Server | `127.0.0.1` |
| Database Name | `dvwa` |
| Database User | `dvwa` |
| Database Port | `3306` |

### Step 7 — Connect to MariaDB

The database command-line client was started with:

```bash
mysql -u dvwa -p
```

The client requested the database password interactively.

The course output identified:

```text
Welcome to the MariaDB monitor. Commands end with ; or \g.

Your MariaDB connection id is 239

Server version: 10.5.19-MariaDB-0+deb11u2 Debian 11
```

The connection was established successfully.

### Step 8 — Identify the Stored Guestbook Records

Within the MariaDB client, the DVWA database was selected:

```sql
use dvwa;
```

The client returned:

```text
Database changed
```

The tables were listed:

```sql
show tables;
```

The result was:

```text
+----------------+
| Tables_in_dvwa |
+----------------+
| guestbook      |
| users          |
+----------------+
2 rows in set (0.001 sec)
```

The guestbook table was then queried:

```sql
select * from guestbook;
```

The supplied output excerpt contains:

```text
+------------+--------------------------------------------------------------+---------+
| comment_id | comment                                                      | name    |
+------------+--------------------------------------------------------------+---------+
| 1          | This is a test comment.                                      | test    |
| 2          | <script>alert(document.cookie);</script>                     | Teste   |
| 3          | [Stored script referencing the laboratory collector]         | José    |
+------------+--------------------------------------------------------------+---------+

11 rows in set (0.001 sec)
```

The supplied course extraction displays three representative records while reporting 11 total rows.

The complete contents of the remaining records were not included in the supplied text.

The table confirms that the application persisted script-bearing content in the guestbook.

### Step 9 — Interpret the Stored Record

The database record containing JavaScript is evidence that the content was stored by the application.

When the vulnerable application retrieves and renders the record, the browser may execute the content again.

The database evidence can be correlated with Apache access logs to identify which users or client IPs accessed the affected page after the script was stored.

## 5. Expected Results

The activity demonstrates that stored XSS leaves persistent evidence in the application database.

| Item | Result |
|---|---|
| Application | DVWA |
| Vulnerable Module | XSS (Stored) |
| Security Level | Low |
| Database | `dvwa` |
| Database Server | MariaDB |
| Database Table | `guestbook` |
| Guestbook Fields | `comment_id`, `comment`, `name` |
| Test Script | JavaScript alert |
| Stored Content | Script-bearing guestbook entries |
| Local Collection Port | `8080` |

The `guestbook` table contains records associated with the XSS test.

## 6. Technical Analysis

### Why Stored XSS Is Persistent

The application stores the submitted message in the database.

When the page displays the guestbook entries, the vulnerable implementation includes the stored value in the HTML response.

If the application fails to encode or sanitize that value appropriately, the browser interprets the script as executable content.

The malicious content can therefore affect users who access the page after the original submission.

### Database Evidence

The database is an important source of evidence in this activity.

The `guestbook` table contains the message submitted by the user.

The record with the JavaScript test confirms that script-bearing content was persisted.

The name and comment identifier help distinguish the affected record from other entries.

### Why the Access Log Is Not Sufficient

The access log records HTTP requests.

For stored XSS, the malicious message may be submitted once and stored in the database.

Subsequent users may simply request the page containing the stored comment.

Their requests do not necessarily include the original script in the URL.

Therefore, the access log alone may not reveal the full payload.

A complete investigation should correlate:

1. Database content.
2. Apache access records.
3. Client IP addresses.
4. Request timestamps.
5. Browser and session evidence.
6. Information from affected users, when available.

### Database Configuration as an Evidence Source

The DVWA configuration file identifies the database server, database name, and database account.

This allows an authorized investigator with appropriate server access to identify the relevant database for examination.

Configuration files may also contain sensitive credentials and should be handled as restricted evidence.

### Defensive Recommendations

Stored XSS can be mitigated through:

- Context-aware output encoding.
- HTML sanitization when rich text is necessary.
- Server-side input validation.
- Avoiding unsafe insertion of untrusted content into HTML.
- Secure template engines and safe output APIs.
- Content Security Policy as an additional protection.
- Appropriate cookie attributes.
- Monitoring suspicious stored content.

Client-side controls such as `maxlength` are not substitutes for server-side validation.

## 7. Results and Interpretation

The activity demonstrated persistent XSS in DVWA.

The browser executed the JavaScript test after the content was submitted and displayed from the guestbook.

The investigation identified the database configuration, connected to MariaDB, selected the `dvwa` database, and examined the `guestbook` table.

The database records preserved script-bearing content, providing direct evidence of the stored payload.

The results demonstrate why database examination is essential when investigating persistent web application attacks.

## 8. Concepts Practiced

- Stored XSS
- Persistent XSS
- DVWA
- JavaScript injection
- Browser cookie exposure
- HTML form validation
- `maxlength`
- Browser developer tools
- Database configuration analysis
- MariaDB
- MySQL client
- `show tables`
- SQL `SELECT`
- Guestbook records
- Database persistence
- Apache access logs
- Evidence correlation
- Session security
- Output encoding
- HTML sanitization

## 9. Evidence

**Required screenshot: Activity 15.3 — Step 8 — PDF page 3.**

The course instructions require the MariaDB output showing the stored guestbook records.

The screenshot should show the database query:

```sql
select * from guestbook;
```

The table output should show the stored records, including the script-bearing comments.

The database password and session tokens should not be exposed in additional public screenshots.

**Evidence description supplied separately:** the initial screenshot summary describes Command Injection. However, the supplied Lesson 15 practical material identifies Activity 15.3 as Stored XSS, not Command Injection. The expected Step 8 evidence is the `guestbook` database query.

Verify that the final PDF contains the correct Activity 15.3 evidence.

[View Class Evidence PDF](../evidences.pdf)

## References

- [OWASP — Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [OWASP — Stored XSS Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [MDN — Cross-Site Scripting](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS)
- [MariaDB — SELECT](https://mariadb.com/kb/en/select/)
- [MariaDB — SHOW TABLES](https://mariadb.com/kb/en/show-tables/)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 15.4](../atividade-15.4-file-upload/README.md)
