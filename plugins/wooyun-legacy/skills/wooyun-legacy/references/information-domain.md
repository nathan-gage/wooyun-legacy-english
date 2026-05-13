# Information Disclosure Domain

## Overview

Information disclosure is an accelerant. 6,446 WooYun cases prove that exposed information can start every other attack type: leaked credentials lead to account takeover, and leaked architecture enables precise exploitation.

**Core principle:** Any information an application exposes beyond what the user needs is a vulnerability. Debug information, stack traces, internal IPs, API keys, source code: each one multiplies attack surface.

## Attack-Pattern Matrix

### Source Code / Configuration Leakage (4,858 cases, 64.7% high severity)

**Systematic discovery checklist:**

```
1. Version-control leakage
   - [ ] /.git/config -> clone through GitHack/git-dumper
   - [ ] /.svn/entries -> SVN repository exposed
   - [ ] /.hg/ -> Mercurial repository
   - [ ] /.bzr/ -> Bazaar repository
   - [ ] /CVS/Root -> CVS repository

2. Backup files
   - [ ] /backup.zip, /backup.tar.gz, /backup.sql
   - [ ] /db.sql, /database.sql, /dump.sql
   - [ ] /web.rar, /www.zip, /site.tar.gz
   - [ ] /[domain].zip, /[domain].sql
   - [ ] /*.bak, /*.old, /*.orig, /*.swp
   - [ ] /WEB-INF/web.xml (Java)
   - [ ] /config.php.bak, /settings.py.bak

3. Debug/test endpoints
   - [ ] ?debug=true, ?debug=1, ?test=1
   - [ ] /debug, /test, /phpinfo.php
   - [ ] /actuator (Spring Boot), /metrics, /health, /env
   - [ ] /trace, /dump, /heapdump
   - [ ] /__debug__/ (Django Debug Toolbar)
   - [ ] /console (Rails console, H2 console)
   - [ ] /swagger-ui.html, /api-docs, /openapi.json

4. Error information
   - [ ] Trigger 500 error -> stack trace containing file paths
   - [ ] Invalid input -> database error containing query structure
   - [ ] Missing parameter -> framework error containing class names
   - [ ] Server version exposed in 404 response headers
```

### Sensitive Data Leakage (1,588 cases, 62.8% high severity)

**Personal information leakage patterns:**

| Leakage vector | Leaked contents | Test method |
|----------------|-----------------|-------------|
| API overfetching | Full user object (password hash, email, phone, ID) | Compare API response with UI display |
| Accessible log files | User activity, queries, credentials | /logs/, /log/, /access.log |
| Error information | Database structure, file paths, internal IPs | Trigger errors with malformed input |
| Client-side storage | Tokens and personal information in localStorage/sessionStorage | Inspect browser developer tools |
| URL parameters | Session tokens and user IDs in Referer header | Check GET parameters for sensitive data |
| Cached responses | Other users' data in CDN/proxy cache | Test Cache-Control headers |
| Export features | Unauthorized bulk data export | Test /export, /download, /report endpoints |

**Key finding indicators:**
- API response field count > UI-visible field count
- Detailed error messages in production
- Server headers exposing versions (`X-Powered-By`, `Server`)
- HTML/JS comments exposing internal information
- Credentials in client-side JavaScript

### Directory/File Enumeration

**High-yield paths (from WooYun statistics):**

```
# Management
/admin/            /manage/           /backend/
/administrator/    /system/           /console/

# Configuration
/config/           /conf/             /settings/
/.env              /wp-config.php     /application.yml

# Data
/upload/           /uploads/          /files/
/data/             /export/           /tmp/

# Monitoring
/status/           /server-status     /server-info
/monitoring/       /metrics/          /grafana/

# Documentation
/api/docs          /swagger/          /redoc/
/readme.md         /README.txt        /CHANGELOG
```

## Real Cases

| Case | Subdomain | Impact |
|------|-----------|--------|
| Dingding rental email leakage exposed information for 600+ people | Personal information leakage | 600+ user records exposed through email |
| Multiple Inke database servers were compromised | Source code/configuration | Multiple database servers compromised |
| Xinnet command execution caused leakage of 450,000 user records | Source code/configuration | 450,000 user records leaked through remote code execution |
| Sunshine Insurance sensitive information leakage led to successful internal-system access, including direct login to multiple operations hosts | Personal information leakage | Internal-network pivot through leaked credentials |
| Transfar Group mail system exposed internal sensitive information | Personal information leakage | Internal mail system exposure |
| TCL system misconfiguration leaked 6 million customer names, mobile numbers, and home addresses | Personal information leakage | 6 million customer personal records |
| Baixing Pharmacy vulnerability endangered 20M personal-detail records, including names, IDs, phone numbers, and addresses | Personal information leakage | 20 million personal information records |

## Defense Patterns

### Code Level
- **Minimize responses:** return only fields the client needs; do not return complete database objects
- **Error handling:** show generic errors only in production; keep details in development only
- **Credential management:** use environment variables or secret stores; never put credentials in code/configuration files
- **Log redaction:** mask personal information in logs, such as email `a***@example.com`

### Architecture Level
- **Enforce .gitignore:** configuration files, .env, and credentials never belong in repositories
- **WAF rules:** block access to /.git, /.svn, /.env, /backup*
- **Response-header hardening:** remove Server, X-Powered-By, X-AspNet-Version
- **CDN configuration:** do not cache authenticated responses

### Monitoring
- **Sensitive path access:** alert when external IPs access /.git, /.env, /admin
- **Bulk data access:** alert on large API responses or high-frequency data requests
- **Error-rate monitoring:** spike in 500 errors indicates possible reconnaissance
- **Credential-leak scanning:** monitor exposed credentials on GitHub/GitLab/Pastebin
