# Information Disclosure Vulnerability Knowledge Base

> Manual English version of the WooYun information disclosure analysis.
> Original analysis: 7,337 information disclosure cases from the 88,636-case WooYun corpus.

Information disclosure is often the first step in a larger compromise chain. The original WooYun cases show that source code, backups, debug endpoints, configuration files, default credentials, logs, cloud metadata, and over-broad API responses frequently expose enough data to pivot into account takeover or server compromise.

## 1. Disclosure Categories

| Category | Typical examples | Impact |
|---|---|---|
| Source and VCS exposure | `.svn`, `.git`, source archives | Source review, credentials, hidden endpoints |
| Configuration leakage | `config.php`, `.env`, `web.config`, `db.properties` | Database and third-party keys |
| Backup files | `www.zip`, `db.sql`, `backup.rar` | Complete data or code exposure |
| Debug interfaces | Stack traces, phpinfo, Spring Boot actuator | Internal paths, secrets, environment |
| API overexposure | Full profile fields, tokens, internal IDs | Privacy breach and IDOR chaining |
| Logs and monitoring | Access logs, error logs, admin logs | Tokens, passwords, internal topology |
| Default credentials | Admin consoles and middleware | Direct login or lateral movement |
| Third-party service leakage | Email, CDN, cloud, payment keys | Cross-system compromise |

## 2. High-Value Files and Endpoints

```text
.git/config
.git/HEAD
.svn/entries
.env
config.php
database.php
settings.py
WEB-INF/classes/application.properties
WEB-INF/web.xml
web.config
phpinfo.php
/actuator/env
/actuator/heapdump
/swagger-ui.html
/api-docs
backup.zip
db.sql
access.log
error.log
```

## 3. Common Exploitation Chains

### Source leak to database compromise

```text
VCS directory exposed -> source download -> database config found
-> database login -> user data or admin credentials exposed
```

### Debug endpoint to secret extraction

```text
Debug endpoint -> environment variables -> cloud/API keys
-> third-party service access -> data export
```

### API overexposure to account takeover

```text
User info API returns phone/email/token -> IDOR or reset flow tested
-> password reset or session takeover
```

### Default credential to internal movement

```text
Middleware console exposed -> default password works
-> deploy shell or read configuration -> internal network pivot
```

## 4. Testing Workflow

1. Enumerate static files, backup names, VCS directories, debug endpoints, API docs, and admin panels.
2. Review API responses for fields not required by the caller: passwords, salts, tokens, full ID numbers, internal IDs, roles, phone numbers, and emails.
3. Trigger controlled errors and observe whether stack traces, SQL errors, paths, or library versions leak.
4. Search JavaScript bundles for endpoints, keys, and source maps.
5. Check cloud and metadata endpoints only in authorized environments.
6. Confirm impact with minimal data samples; do not dump large datasets.

## 5. Defensive Patterns

- Block VCS directories, backups, and temporary files at the web server layer.
- Keep secrets out of source and build artifacts.
- Disable debug endpoints in production or protect them with strong authentication.
- Return only fields required by the current user and workflow.
- Mask personal data by default.
- Enforce pagination limits and authorization checks on exports.
- Rotate credentials after any exposure.
- Add CI checks for committed secrets and deployed backup artifacts.

## 6. Reporting Checklist

```text
Title: Sensitive information disclosure through [file/API/debug endpoint]
Location: [URL, path, or endpoint]
Data exposed: [types of secrets or personal data]
Access requirement: [none/user/admin/internal]
Impact: [privacy, credential reuse, source disclosure, pivot path]
Proof: [minimal redacted sample]
Remediation: [remove artifact, restrict endpoint, rotate secrets, minimize fields]
```

## 7. Lessons from WooYun Cases

- "Low" information leakage often becomes high impact when it exposes credentials or source code.
- Source disclosure makes later vulnerability discovery much faster.
- API overexposure is a business logic issue, not only a privacy issue.
- Publicly reachable debug and management endpoints are recurring root causes.
