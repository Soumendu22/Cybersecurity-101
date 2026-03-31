# Directory Traversal

## Overview

Directory Traversal allows attackers to access files outside the intended directory by manipulating path input (for example using `../`).

---

## Typical Vulnerable Pattern

Application expects:

- `/download?file=report.pdf`

Attacker tries:

- `/download?file=../../../../etc/passwd`

---

## Impact

- Exposure of sensitive system files
- Leakage of application secrets and configs
- Access to credentials, keys, source code

---

## Common Bypass Techniques

- URL encoding (`..%2f`)
- Double encoding
- Mixed separators (`..\`)
- Null-byte tricks on legacy stacks

---

## Prevention

1. Avoid direct user-controlled filesystem paths.
2. Use allowlisted filenames or IDs mapped server-side.
3. Canonicalize and validate path against approved base directory.
4. Deny path traversal sequences after normalization.
5. Run service with least filesystem permissions.

---

## Testing Checklist

- Can `../` escape base directory?
- Are encoded traversal payloads blocked?
- Are absolute paths accepted unexpectedly?
- Can traversal reach app configs or key material?

---

## Practice Tasks

1. Test traversal in a lab download endpoint.
2. Implement secure path normalization and allowlists.
3. Verify bypass attempts with encoded payload variants.
4. Restrict file permissions to minimize impact.
5. Add automated tests for traversal regression.

---

## Why Path Normalization Is Tricky

- Different OS path separators (`/` vs `\\`)
- URL decoding order and double decoding issues
- Unicode normalization edge cases
- Archive extraction and symlink traversal behavior

If normalization and validation happen in the wrong order, bypasses are likely.

---

## Secure File Access Pattern

1. Accept only resource IDs from clients.
2. Resolve ID to server-side file metadata.
3. Build canonical absolute path internally.
4. Ensure path starts with approved base directory.
5. Deny symlink escapes and log rejected attempts.

---

## Related Weakness Chains

- Traversal + file upload = executable placement risk
- Traversal + weak logs = credential leakage
- Traversal + backup exposure = source code disclosure

---

## Monitoring and Detection

- Alert on repeated path traversal signatures.
- Track high-rate requests to download/read endpoints.
- Detect unusual access to config/secret file names.
- Correlate with authentication anomalies.

---

## Remediation Playbook

1. Patch affected endpoint with strict server-side mapping.
2. Rotate any exposed credentials/secrets.
3. Review access logs for exfiltration indicators.
4. Add regression tests for encoded and mixed-separator payloads.
5. Include secure path handling in coding standards.
