# Activity 12.1 — Browser History Investigation

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 02  
> **Course Lesson:** 12  
> **Environment:** forenseWin VM  
> **Status:** Completed

## 1. Objective

Examine a Microsoft Edge browsing history database and identify browsing records associated with the group Anonymous.

The activity uses the SQLite database `History.db`, recovered from the forensic material supplied for the investigation.

The database is examined with DB Browser for SQLite, focusing on the `urls` table.

The investigation consists of:

- Opening the recovered SQLite database.
- Listing the browsing records stored in the `urls` table.
- Filtering URLs containing the keyword `anonymous`.
- Converting the Edge timestamp into a readable UTC date and time.
- Examining the time interval between the first and last records.

The purpose is to identify browsing activity that may help correlate the investigated user with the group referenced in the case study.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseWin` |
| Operating System | Windows |
| VM Address | `192.168.98.30` |
| Forensic Application | DB Browser for SQLite |
| Database Engine | SQLite |
| Database File | `History.db` |
| Source Directory | `C:\curso\aula12` |
| Database Path | `C:\curso\aula12\History.db` |
| Main Table | `urls` |
| SQL Interface | Execute SQL |
| Investigation Keyword | `anonymous` |

The course provides the Windows forensic workstation and the recovered browser history database.

## 3. Browser History and SQLite Concepts

### Browser History as Forensic Evidence

Browser history can provide information about a user's browsing activity.

Depending on the browser and the information retained, the history database may contain:

- Visited URLs.
- Page titles.
- Visit counts.
- Last visit timestamps.
- Transition information.
- Other browsing metadata.

These records can help reconstruct user activity and identify searches or visits related to an investigation.

However, browser history must be interpreted in context. A URL entry alone does not prove who initiated the visit or establish the user's intent.

### SQLite Database

SQLite is an embedded relational database engine used by many applications.

Instead of storing information in a conventional collection of text files, an application can maintain structured records inside a database file.

The Microsoft Edge history database uses SQLite.

For this exercise, the database file is:

```text
C:\curso\aula12\History.db
```

### DB Browser for SQLite

DB Browser for SQLite provides a graphical interface for inspecting SQLite databases.

The application allows the analyst to:

- Open an existing database.
- Browse database tables.
- Inspect stored records.
- Execute SQL statements.
- Review the results returned by queries.

The activity uses the `Execute SQL` tab to query the `urls` table.

### Edge Timestamp Format

Chromium-based browsers use timestamps based on microseconds since January 1, 1601 UTC.

This is different from the Unix timestamp, which counts seconds since January 1, 1970 UTC.

The `last_visit_time` field therefore requires conversion before it can be interpreted as an ordinary date and time.

## 4. Procedure

### Step 1 — Open the Recovered History Database

The Windows forensic workstation was accessed.

DB Browser for SQLite was opened from the available applications.

The following menu path was selected:

```text
File → Open Database
```

The recovered database was selected:

```text
C:\curso\aula12\History.db
```

After opening the database, its internal structure was displayed.

The database contains multiple tables. For this investigation, the analysis focuses on:

```text
urls
```

The `urls` table stores URL-related browsing records.

### Step 2 — Display All Records from the URLs Table

The `Execute SQL` tab was selected.

The following SQL statement was executed:

```sql
SELECT * FROM urls;
```

The query returns all columns and records from the `urls` table.

According to the course material, the result contained:

```text
16 rows
```

The records included browsing information associated with the user.

The purpose of this first query was to understand the available records before applying a filter.

### Step 3 — Filter Records Related to Anonymous

To identify browsing records that could be relevant to the investigation, the following query was executed:

```sql
SELECT *
FROM urls
WHERE url LIKE "%anonymous%";
```

The query uses the SQL `LIKE` operator to search the `url` column.

The wildcard character `%` represents any sequence of characters before or after the search term.

The expression:

```sql
LIKE "%anonymous%"
```

therefore selects URLs containing the keyword `anonymous` anywhere in the field.

The result contained:

```text
6 matching records
```

The six matches were considered relevant to the case study because they contained the keyword associated with the investigated group.

The relatively small number of browsing records was also noted. The course material suggests that this may indicate frequent history deletion, although the number of records alone is not sufficient to prove that the user regularly deleted browsing history.

### Step 4 — Convert Edge Timestamps to UTC Date and Time

The `last_visit_time` column contains timestamps represented as microseconds since January 1, 1601 UTC.

To make these values readable, the following SQL query was executed:

```sql
SELECT *,
       datetime(
           last_visit_time / 1000000 +
           (strftime('%s', '1601-01-01')),
           'unixepoch'
       ) AS date
FROM urls;
```

The query performs the conversion in several stages:

| Expression | Function |
|---|---|
| `last_visit_time / 1000000` | Converts microseconds into seconds |
| `strftime('%s', '1601-01-01')` | Obtains the Unix timestamp corresponding to the beginning of the Windows/Chromium epoch |
| Addition of both values | Converts the Edge timestamp to Unix time |
| `datetime(..., 'unixepoch')` | Formats the resulting value as a readable date and time |
| `AS date` | Names the resulting column `date` |

The query adds a readable date column to the returned records.

The course material identifies the following results:

| Record | Converted UTC Timestamp |
|---|---|
| First record | `2023-06-11 15:57:52` |
| Last record | `2023-06-11 15:59:47` |

The two timestamps are separated by approximately 1 minute and 55 seconds.

The conversion query returns UTC values. When representing the same timestamps in Brasília time (UTC-3), the corresponding times are:

| Record | UTC | Brasília Time |
|---|---|---|
| First record | `15:57:52` | `12:57:52` |
| Last record | `15:59:47` | `12:59:47` |

The original values returned by the SQL query should be preserved as UTC.

## 5. Expected Results

The activity produces three relevant query results:

| Query | Expected Result |
|---|---|
| `SELECT * FROM urls;` | 16 browsing records |
| `SELECT * FROM urls WHERE url LIKE "%anonymous%";` | 6 matching records |
| Timestamp conversion query | Readable UTC date and time column |

The first and last records are identified as:

```text
2023-06-11 15:57:52 UTC
2023-06-11 15:59:47 UTC
```

These records establish a short interval between the beginning and end of the browsing activity represented in the database.

## 6. Technical Analysis

### Why Use the URLs Table?

The `urls` table provides URL-related browsing records that can be queried directly.

Filtering this table allows the analyst to reduce the amount of information examined and focus on entries relevant to the investigation.

The search for `anonymous` was used as an investigative filter rather than as proof of group membership.

### SQL LIKE Operator

The query:

```sql
SELECT *
FROM urls
WHERE url LIKE "%anonymous%";
```

uses a partial string match.

The `%` wildcard is useful when the exact URL is unknown but a relevant keyword is available.

This approach can identify URLs containing the target term in different positions.

### Chromium Timestamp Conversion

The timestamp stored in `last_visit_time` is based on a different epoch from Unix time.

The value is stored as microseconds, whereas Unix time is normally represented in seconds.

The conversion therefore requires:

1. Dividing the original value by one million.
2. Adding the Unix timestamp offset corresponding to January 1, 1601.
3. Formatting the result with SQLite's `datetime` function.

The query produces a readable timestamp without requiring manual conversion of every record.

### Interpreting the Time Interval

The first and last converted timestamps are separated by approximately 115 seconds.

This is a short period for the browsing activity represented by the records.

The course material suggests that the short interval and limited number of records may be consistent with a user who frequently clears browsing history.

That interpretation should remain a hypothesis. Other possibilities include a newly created browser profile, limited browser use, or an incomplete recovered database.

Additional artifacts would be required to establish whether browsing history was deliberately deleted.

## 7. Results and Interpretation

The recovered database contained 16 rows in the `urls` table.

Filtering the records with the keyword `anonymous` returned six matches.

The timestamp conversion query identified the first and last records as:

```text
2023-06-11 15:57:52 UTC
2023-06-11 15:59:47 UTC
```

The records show browsing activity related to the keyword used in the investigation within a short time interval.

The results provide an investigative lead that can be correlated with other artifacts recovered from the seized devices.

The database does not independently identify the person who performed the searches or establish their relationship with the group.

## 8. Concepts Practiced

- Browser forensics
- Microsoft Edge history
- Chromium timestamp format
- SQLite databases
- DB Browser for SQLite
- SQL queries
- `SELECT`
- `WHERE`
- `LIKE`
- Wildcard filtering
- `strftime`
- `datetime`
- Unix timestamp conversion
- UTC timestamps
- Browsing activity reconstruction
- Digital evidence correlation

## 9. Evidence

**Required screenshot: Print 1 — PDF page 1 — Step 4.**

The screenshot must show the DB Browser for SQLite interface with the timestamp conversion query executed.

The evidence should demonstrate:

- The `Execute SQL` tab.
- The SQL statement used to convert `last_visit_time`.
- The resulting `date` column.
- The readable UTC timestamps.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 12.1 is on page 1 of the consolidated PDF.

## References

- [SQLite — Date and Time Functions](https://www.sqlite.org/lang_datefunc.html)
- [DB Browser for SQLite — Execute SQL Tab](https://sqlitebrowser.org/blog/execute-sql-tab-overhaul/)
- [Chromium — Time Representation and Windows Epoch](https://chromium.googlesource.com/chromium/src/+/refs/heads/main/base/time/time.h)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 12.2](../atividade-12.2-diretorios-usuario/README.md)
