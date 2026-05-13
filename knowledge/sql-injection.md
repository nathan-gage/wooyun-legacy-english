# SQL Injection Vulnerability Analysis Methodology

> Manual English version of the WooYun SQL injection methodology.
> Original data source: 27,732 SQL injection cases from `wooyun_vulnerabilities.json`.

SQL injection is a boundary failure between data and executable SQL. The WooYun cases show recurring patterns across login forms, search boxes, GET and POST parameters, cookies, headers, admin systems, CMS modules, and industry-specific business systems.

## 1. Core Model

```text
Missing input validation -> dynamic SQL concatenation -> syntax boundary break -> database instruction execution
```

The attack succeeds when attacker-controlled input is interpreted as SQL rather than data.

## 2. Injection Entry Points

| Vector | Typical scenario |
|---|---|
| Login fields | Username and password concatenated into SQL |
| Search fields | `LIKE` queries and filters |
| GET parameters | Detail pages, category IDs, paging, sorting |
| POST parameters | Forms, callbacks, admin actions |
| HTTP headers | `User-Agent`, `Referer`, `X-Forwarded-For` |
| Cookies | Session or tracking values used in queries |
| JSON bodies | Nested IDs and filter objects |

High-risk parameter names:

```text
id, uid, userId, aid, type, typeid, categoryid, sort_id, stid,
fid, page, action, act, username, password, name, keyword,
__VIEWSTATE, __EVENTVALIDATION, __EVENTARGUMENT, __EVENTTARGET
```

## 3. URL and File-Type Patterns

```text
/news/detail.php?id=1
/product/view.aspx?pid=123
/article.asp?aid=456
/search.php?keyword=test
/admin/login.aspx
/api/getData.php?type=user&id=1
```

| File type | Common database |
|---|---|
| `.php` | MySQL |
| `.aspx` | MSSQL or Oracle |
| `.asp` | Access or MSSQL |
| `.jsp`, `.do`, `.action` | Oracle or MySQL |

## 4. Database Fingerprinting

### MySQL

```sql
AND @@version LIKE '%MySQL%'
AND version() IS NOT NULL
AND sleep(5)
AND (SELECT 1 FROM information_schema.tables LIMIT 1)
```

### MSSQL

```sql
AND @@version LIKE '%Microsoft%'
AND db_name() IS NOT NULL
WAITFOR DELAY '0:0:5'
AND (SELECT 1 FROM sysobjects WHERE xtype='U')
```

### Oracle

```sql
AND (SELECT banner FROM v$version WHERE rownum=1) IS NOT NULL
AND 1=(SELECT 1 FROM dual)
```

### PostgreSQL

```sql
AND version() LIKE '%PostgreSQL%'
AND pg_sleep(5) IS NULL
```

## 5. Injection Types

| Type | Signal |
|---|---|
| Error-based | Database error reveals syntax or data |
| Boolean blind | Response changes for true/false conditions |
| Time blind | Delay indicates condition result |
| UNION query | Attacker-selected rows appear in response |
| Stacked queries | Additional statements execute |
| Out-of-band | DNS or HTTP callback confirms execution |

## 6. WAF and Filter Bypass Families

### Inline comments

```sql
UNION/**/SELECT/**/1,2,3
/*!50000UNION*/ /*!50000SELECT*/ 1,2,3
```

### Encoding and case changes

```text
%55%4e%49%4f%4e
UnIoN SeLeCt
```

### Whitespace alternatives

```sql
UNION%0aSELECT
UNION%09SELECT
```

### Quote avoidance

```sql
CHAR(97,100,109,105,110)
0x61646d696e
```

### Wide-byte and escaping bypass

```text
%bf%27
```

This applies to GBK or similar encodings where `addslashes()` can be bypassed by malformed multibyte sequences.

## 7. Safe Testing Workflow

1. Identify parameters and their data type.
2. Send harmless syntax probes such as a single quote or numeric boolean changes.
3. Fingerprint database type only after confirming a signal.
4. Use minimal extraction to prove impact; do not dump data.
5. Document the vulnerable sink and the exact query construction pattern if source is available.

## 8. Vulnerable Code Patterns

### PHP

```php
$id = $_GET['id'];
$sql = "SELECT * FROM news WHERE id=$id";
```

### ASP

```vb
sql = "select * from users where id=" & Request("id")
```

### Java

```java
String sql = "select * from users where name='" + request.getParameter("name") + "'";
Statement st = conn.createStatement();
```

## 9. Remediation

- Use prepared statements with bound parameters.
- Convert numeric IDs to integers before use.
- Use allowlists for sort fields, table names, and directions.
- Never concatenate request values into SQL.
- Apply least privilege to database accounts.
- Centralize query helpers and forbid raw SQL construction in handlers.
- Log and rate-limit injection probes.

Prepared statement example:

```java
PreparedStatement ps = conn.prepareStatement(
    "SELECT * FROM users WHERE id = ?"
);
ps.setInt(1, id);
```

## 10. Reporting Checklist

```text
Title: SQL injection in [endpoint/parameter]
Parameter: [name and location]
Database signal: [error, boolean, time, UNION, OOB]
Payload: [minimal proof]
Impact: [data read/write, auth bypass, DBA privileges]
Root cause: [dynamic SQL concatenation]
Remediation: [prepared statements, allowlists, least privilege]
```

## 11. Lessons from WooYun Cases

- Reused CMS code creates repeated vulnerabilities across many sites.
- Subsite injection can become enterprise-wide compromise when credentials are reused.
- Login-required injection is still high risk because any normal account can reach it.
- Payment callbacks and business forms often have less mature SQL filtering than public search pages.
