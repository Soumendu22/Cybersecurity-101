# File Upload Security

## Overview

File upload features are high risk. Weak validation can enable remote code execution, malware hosting, data overwrite, or storage abuse.

---

## Common Risks

- Uploading executable scripts (webshells)
- MIME/content-type spoofing
- Extension bypasses (`.php.jpg`, `.phtml`)
- Path traversal in filename
- Overwriting existing files
- Malicious document payloads

---

## Secure Upload Pipeline

1. Require authentication and authorization.
2. Enforce strict allowlist by type and extension.
3. Validate real file signature (magic bytes), not just extension.
4. Rename files to random server-generated names.
5. Store uploads outside web root when possible.
6. Scan files with anti-malware/content inspection.
7. Serve downloads with safe headers and controlled handlers.

---

## Storage and Execution Controls

- Separate upload storage service/bucket
- Disable script execution in upload directories
- Restrict permissions to minimum needed
- Apply size and rate limits

---

## Testing Checklist

- Can executable content be uploaded and executed?
- Can extension/MIME checks be bypassed?
- Are filenames sanitized safely?
- Can path traversal overwrite critical files?
- Are large file abuse and DoS paths controlled?

---

## Practice Tasks

1. Try extension and content-type bypasses in a lab app.
2. Implement magic-byte validation.
3. Configure non-executable upload storage policy.
4. Add anti-malware scan stage and fail-safe behavior.
5. Create security tests for upload validation bypasses.

---

## Advanced Bypass Patterns

- Double extensions and parser confusion
- Polyglot files valid in multiple formats
- Case sensitivity and unicode filename tricks
- Archive bombs and nested compression abuse
- Metadata payload abuse in image/document parsers

---

## Secure Upload Architecture

1. Upload to temporary quarantine area.
2. Validate type, structure, and size limits.
3. Scan with malware and content policy engines.
4. Re-encode or sanitize risky formats when possible.
5. Move approved files to immutable object storage.
6. Serve files from separate domain with strict content headers.

---

## Response Header Safety for Downloads

- `Content-Disposition: attachment` for untrusted content
- `X-Content-Type-Options: nosniff`
- Strict `Content-Type` assignment from validated metadata

These controls reduce browser-side execution risk.

---

## Monitoring and Incident Response

- Alert on upload validation failures and repeated bypass attempts.
- Monitor execution events originating from upload paths.
- Keep hash inventory for uploaded files and scan history.
- Build takedown workflow for malicious uploaded content.

---

## Compliance and Data Governance Notes

- Define retention and deletion rules for uploaded content.
- Classify sensitive uploads and apply encryption at rest.
- Restrict internal access to file processing pipelines.
- Audit access logs for sensitive document downloads.
