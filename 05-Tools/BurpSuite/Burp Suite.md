# Burp Suite

## Overview

Burp Suite is a web security testing platform for intercepting traffic, discovering attack surface, and validating vulnerabilities in web applications and APIs.

---

## Core Modules

- Proxy: intercept and modify HTTP(S) requests
- Repeater: manual request testing
- Intruder: payload automation
- Scanner (Pro): automated vulnerability scanning
- Decoder/Comparer: encode/decode and response analysis
- Collaborator (Pro): out-of-band interaction testing

---

## Setup and Proxy Configuration

1. Start Burp and open Proxy listener (default 127.0.0.1:8080).
2. Configure browser proxy to Burp listener.
3. Install Burp CA certificate for HTTPS interception.

---

## Essential Workflow

1. Browse target through Proxy and map endpoints.
2. Send interesting requests to Repeater.
3. Manipulate parameters, headers, cookies.
4. Use Intruder for controlled fuzzing.
5. Document exploitable behavior with request/response evidence.

---

## Useful Testing Patterns

### Authentication and Session

- Test login error messages for enumeration
- Check session cookie flags (`HttpOnly`, `Secure`, `SameSite`)
- Verify session invalidation on logout/password change

### Access Control

- Modify IDs for IDOR checks
- Replay low-privilege tokens on admin routes
- Test HTTP verb tampering

### Input Validation

- Inject payloads in URL, body, headers
- Observe reflection, encoding, and response timing
- Compare normal vs malicious response deltas

---

## Repeater Tips

- Keep baseline request tab unchanged
- Clone per test case
- Mark hypotheses in tab names
- Compare responses by status, length, key strings

---

## Intruder Tips

- Use sniper for single-parameter fuzzing
- Use cluster bomb for multi-parameter logic testing
- Add grep match/extract rules for clear result triage
- Keep request rate controlled to avoid noise

---

## API Testing with Burp

- Import OpenAPI/Swagger definitions where available
- Test JSON schema edge cases
- Validate auth scopes and object-level authorization
- Check CORS, rate limits, and error handling consistency

---

## Burp CLI/Automation Notes

Burp is primarily GUI-driven, but you can combine it with:

- project files for reproducibility
- extension ecosystem (BApp store)
- external scripts for post-processing findings

---

## Evidence Collection Checklist

- Full raw request and response
- Authentication context used
- Steps to reproduce
- Impact description
- Suggested remediation

---

## Practice Tasks

1. Intercept and modify a login flow in a lab app.
2. Test IDOR by editing object IDs in Repeater.
3. Build Intruder payload set for parameter fuzzing.
4. Validate CSRF protection behavior manually.
5. Export evidence and write a concise finding report.
