# Cross-Site Scripting (XSS)

## Overview

XSS occurs when untrusted input is interpreted as executable script in a victim's browser. It can lead to session theft, account takeover, phishing overlays, and client-side malware behavior.

---

## XSS Types

### Stored XSS

Malicious payload is persisted (database/comments/profile) and served to other users.

### Reflected XSS

Payload is reflected in immediate response from URL/query/body input.

### DOM-Based XSS

Client-side JavaScript manipulates unsafe sources into dangerous sinks.

---

## Common Sources and Sinks

Sources:

- URL params
- hash fragments
- form fields
- postMessage data

Dangerous sinks:

- `innerHTML`
- `document.write`
- `eval` and dynamic code APIs
- inline event handlers

---

## Impact

- Session theft (if token accessible)
- CSRF token exfiltration
- Keystroke logging
- Defacement
- Malicious actions as victim user

---

## Prevention Strategy

1. Context-aware output encoding:
   - HTML body encoding
   - HTML attribute encoding
   - JavaScript string encoding
   - URL encoding
2. Use safe templating defaults (auto-escaping).
3. Sanitize rich HTML with trusted libraries.
4. Avoid dangerous sinks in frontend code.
5. Deploy strong Content Security Policy (CSP).

---

## CSP as Defense-in-Depth

Example baseline direction:

- disallow inline scripts
- allow scripts only from trusted origins
- use nonce/hash for controlled inline usage

CSP is not a replacement for output encoding.

---

## Testing Workflow

1. Identify reflected and stored input points.
2. Determine rendering context (HTML/attribute/JS/URL).
3. Test context-specific payload behaviors safely.
4. Check for filter bypasses and encoding gaps.
5. Validate exploitability and business impact.

---

## Secure Development Checklist

- No raw `innerHTML` with untrusted data
- Centralized encoding helper functions
- Framework safe-binding patterns only
- CSP in report-only then enforcement mode
- Security tests for all user-controlled rendering paths

---

## Practice Tasks

1. Find and classify XSS points in a deliberately vulnerable lab app.
2. Fix each issue using proper context encoding.
3. Replace unsafe DOM sinks with safe alternatives.
4. Add and test a CSP policy.
5. Create regression tests for previously exploitable routes.

---

## Framework-Aware XSS Notes

- Modern frameworks reduce XSS risk with auto-escaping, but unsafe escape hatches still exist.
- Direct DOM manipulation and third-party widgets can bypass framework safety guarantees.
- Markdown/rich-text rendering paths require explicit sanitization design.

---

## Trusted Types and DOM Hardening

For complex frontends:

- Adopt Trusted Types policies where supported.
- Block unsafe inline script patterns.
- Replace dangerous DOM APIs with safe text insertion methods.

This significantly reduces DOM-based XSS classes.

---

## XSS to Account Takeover Chain

Typical chain:

1. Inject script into trusted origin.
2. Perform sensitive actions via victim session context.
3. Exfiltrate non-cookie sensitive data (if accessible).
4. Persist access via profile/API token changes.

Defense requires both output safety and robust session/account controls.

---

## Monitoring and Detection

- CSP report collection and triage.
- Alert on sudden client-side error spikes in render paths.
- Detect suspicious reflected parameters in logs.
- Monitor high-risk account-change endpoints for unusual behavior.

---

## Remediation Process

1. Identify source and rendering context.
2. Apply context-appropriate encoding/sanitization.
3. Remove unsafe sinks and add code-level guards.
4. Add regression tests for payload classes.
5. Roll out CSP improvements and monitor reports.
