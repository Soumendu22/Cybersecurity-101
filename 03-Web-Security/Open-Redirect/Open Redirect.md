# Open Redirect

## Overview

Open Redirect occurs when a web app redirects users to attacker-controlled URLs without strict validation.

---

## Why It Matters

Open redirects are often used for:

- phishing with trusted domain appearance
- OAuth token leakage in misconfigured flows
- chaining with other attacks

---

## Vulnerable Pattern

- `/redirect?next=https://evil.example`

If `next` is not validated against allowlist, abuse is possible.

---

## Prevention

1. Use server-side route names instead of full user-supplied URLs.
2. If external redirects are needed, enforce strict allowlist.
3. Block scheme-relative and obfuscated URL forms.
4. Normalize and validate redirect target before use.
5. Show intermediate warning page for external destinations.

---

## Testing Checklist

- Are full external URLs accepted in redirect params?
- Can encoded/obfuscated payloads bypass validation?
- Can protocol-relative URLs (`//evil`) bypass controls?
- Do redirects interact dangerously with auth/OAuth flows?

---

## Practice Tasks

1. Enumerate all redirect endpoints and parameters.
2. Test encoded and obfuscated redirect payloads.
3. Implement strict allowlist validation logic.
4. Add safe fallback route when validation fails.
5. Validate OAuth redirect URI protections end to end.

---

## Validation Edge Cases to Handle

- URL-encoded bypass attempts
- Double-encoded target values
- Protocol-relative targets (`//example`)
- Userinfo confusion (`trusted.com@attacker.com`)
- Mixed scheme/domain tricks and unicode homographs

Normalization must happen before validation, not after.

---

## OAuth and SSO Risk Amplification

Open redirects become more serious when tied to authentication flows:

- token/code leakage through redirect chains
- phishing flows that appear fully legitimate
- trust abuse against identity provider callback handling

Use exact match callback allowlists with strict scheme, host, and path.

---

## Secure Redirect Design

1. Accept only internal route keys (for example `dashboard`, `billing`).
2. Map keys to server-defined destinations.
3. Ignore arbitrary external URLs by default.
4. For permitted external redirects, maintain signed allowlist entries.
5. Log all rejected redirect attempts for abuse detection.

---

## Detection and Monitoring

- Monitor sudden spikes in redirect parameter abuse.
- Alert on redirects to newly seen external domains.
- Correlate suspicious redirects with phishing reports.
- Include redirect endpoint review in release security checks.
