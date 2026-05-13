# File Upload Vulnerability Analysis Manual

> Manual English version of the WooYun file upload knowledge base.
> Original source: 2,711 WooYun file upload cases, with detailed payload and bypass matrices.

File upload vulnerabilities are rarely "just upload bugs." They are validation failures that let attacker-controlled bytes reach an executable, interpretable, or sensitive location. This manual keeps the original emphasis on extension checks, MIME checks, file content checks, parser behavior, race windows, and server configuration.

## 1. Upload Attack Surface

| Surface | Typical failure |
|---|---|
| Avatar and profile images | Client-side validation only; image parser exploit |
| Attachments and documents | Dangerous extensions accepted; preview converter exploit |
| Rich text editor uploads | Known editor paths and weak extension filters |
| Import/export features | Uploaded archive expands to unsafe paths |
| Admin-only upload tools | Low-privilege users reach admin upload APIs |
| Mobile/API uploads | Missing server-side checks because the client enforces rules |

## 2. Validation Layers

```text
Client JavaScript -> extension check -> MIME check -> file header check
-> content scan -> storage path -> execution configuration -> access control
```

Most WooYun cases failed because one layer was treated as complete security. The correct model is layered validation plus a non-executable storage location.

## 3. Extension Bypass Matrix

| Technique | Examples |
|---|---|
| Case changes | `.pHp`, `.JSP`, `.AsPx` |
| Double extensions | `shell.php.jpg`, `shell.jsp;.jpg` |
| Alternate executable extensions | `.phtml`, `.php5`, `.asa`, `.cer`, `.jspx` |
| Null byte truncation | `shell.php%00.jpg` |
| Trailing dots/spaces | `shell.asp.`, `shell.php ` |
| Parser confusion | `/upload/shell.asp/1.jpg`, `/image.jpg/shell.php` |
| Unicode or encoding tricks | URL-encoded dots and slashes |

## 4. MIME and Content-Type Bypass

MIME type is supplied by the client unless the server independently detects it.

```http
Content-Disposition: form-data; name="file"; filename="shell.php"
Content-Type: image/jpeg

<?php echo shell_exec($_GET['cmd']); ?>
```

Defensive rule: MIME type can support UX decisions, but must not be the trust anchor. Use independent file-type detection, strict allowlists, and safe storage.

## 5. File Header and Image Checks

Attackers commonly add valid-looking magic bytes to executable content.

```text
GIF89a
<?php echo "test"; ?>
```

Image dimension checks can also be bypassed with polyglot files or malformed images. Even a valid image can become dangerous if the server later includes it through LFI or routes it to an unsafe parser.

## 6. Server Parsing Risks

| Server or stack | Risk pattern |
|---|---|
| IIS 6.0 | `folder.asp/file.jpg` parsing |
| Apache misconfiguration | Multi-extension parsing such as `.php.jpg` |
| Nginx plus PHP-CGI | Path-info parsing issues |
| Tomcat/JSP | JSP/JSPX upload and execution |
| PHP include chains | Uploaded image later included as PHP |
| ImageMagick/FFmpeg | Media processing RCE or SSRF |

## 7. Known Product Patterns

WooYun cases repeatedly involved rich text editors, office automation systems, CMS upload components, and collaboration platforms. Common examples include eWebEditor paths, OA drag-page upload handlers, spreadsheet import endpoints, and CMS plugin upload directories.

The transferable lesson is to fingerprint upload components and then test their known storage paths, extension rules, and parser behavior.

## 8. Testing Workflow

1. Enumerate upload endpoints from UI, API traffic, JavaScript, and documentation.
2. Identify accepted extensions, MIME checks, storage path, rename behavior, and returned URL.
3. Test harmless proof files first, then extension, MIME, header, and double-extension variants.
4. Check whether uploaded files are directly reachable and whether the server executes them.
5. Test race windows where files are stored before scanning or deletion.
6. Test whether uploaded files can be included, previewed, converted, or parsed by another component.

## 9. Safe Proof Strategy

Use benign markers when possible:

```php
<?php echo "upload-proof"; ?>
```

For JSP:

```jsp
<% out.println("upload-proof"); %>
```

Avoid destructive commands. In reports, prove execution with a controlled marker, not persistence.

## 10. Race Condition Pattern

Some applications upload the file, then scan or delete it. If the file is reachable during that window, repeated requests can execute it before cleanup.

Defense: scan before publishing, store files in a non-executable quarantine area, use atomic promotion after validation, and serve downloads through application code instead of web-root paths.

## 11. Secure Upload Architecture

- Store uploads outside the web root.
- Generate server-side object names; never trust client file names.
- Use strict allowlists by business need.
- Validate extension, MIME, magic bytes, dimensions, and content where applicable.
- Strip metadata and re-encode images.
- Serve files through an authorization-checked download endpoint.
- Disable script execution in upload directories.
- Monitor upload directories for executable extensions and unusual access patterns.

## 12. Report Template

```text
Title: Unsafe file upload permits [execution/read/overwrite]
Endpoint: [URL and method]
Validation bypass: [extension, MIME, content, race, parser behavior]
Stored location: [path or returned URL]
Proof: [benign marker or controlled execution output]
Impact: [web shell, file overwrite, SSRF, data exposure]
Root cause: [trusted client-side or incomplete validation]
Remediation: [safe storage, allowlist, re-encoding, no execution]
```

## 13. Key Takeaways

- Front-end validation is user experience, not security.
- Blacklists fail because extension and parser variants are numerous.
- MIME values are client-controlled and must be independently verified.
- Upload security is complete only when storage, validation, parser configuration, and access control all hold.
