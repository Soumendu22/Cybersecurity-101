# CORS Misconfiguration

## Overview

Cross-Origin Resource Sharing (CORS) controls which origins can read responses from a different origin in browsers. Misconfigurations can expose sensitive API responses to attacker-controlled websites.

---

## Common Misconfigurations

- `Access-Control-Allow-Origin: *` with sensitive data
- Reflecting arbitrary Origin values
- `Access-Control-Allow-Credentials: true` with broad origins
- Overly permissive methods/headers

---

## Impact

- Cross-origin data theft from authenticated APIs
- Account data exposure via victim browser session
- Increased exploitability with XSS/phishing chains

---

## Secure CORS Policy

1. Allowlist exact trusted origins.
2. Do not use wildcard for credentialed endpoints.
3. Only allow required methods/headers.
4. Validate origin server-side robustly.
5. Keep sensitive endpoints same-origin where possible.

---

## Testing Checklist

- Does server reflect attacker Origin?
- Are credentials allowed cross-origin unexpectedly?
- Are preflight rules broader than intended?
- Do public and private endpoints share unsafe policy?

---

## Practice Tasks

1. Map CORS headers for all API endpoints.
2. Test Origin reflection and credential behavior.
3. Separate public and authenticated CORS policies.
4. Add strict allowlist and verify preflight behavior.
5. Create regression tests for CORS policy drift.

---

## Preflight and Browser Behavior Details

Preflight (`OPTIONS`) requests are used when requests are not "simple" (for example custom headers or non-simple methods).

Important points:

- Browsers enforce CORS; servers and backend clients usually do not.
- `Access-Control-Allow-Origin` must match the requesting origin exactly when credentials are enabled.
- `Vary: Origin` is important for caching correctness.

If cache behavior is wrong, one tenant's CORS policy can accidentally affect another response path.

---

## Common Misconfiguration Patterns in APIs

- Global middleware applies permissive CORS to all routes including admin APIs.
- Staging/debug domains are left in production allowlists.
- Regex allowlists accept attacker-controlled subdomains unexpectedly.
- Private endpoints and public CDN endpoints share one policy.

---

## Secure Implementation Pattern

1. Maintain environment-specific origin allowlists.
2. Evaluate origin per route group (public vs authenticated vs admin).
3. Reject unknown origins explicitly and log denies.
4. Send minimal `Access-Control-Allow-Methods` and headers.
5. Review CORS policy in architecture/security review.

---

## Detection and Monitoring

- Alert on unexpected new allowed origins.
- Track denied cross-origin requests for abuse trends.
- Audit CORS headers during CI/CD integration tests.
- Include CORS checks in API gateway policy scans.

---

## Remediation Playbook

1. Identify all routes returning CORS headers.
2. Classify data sensitivity per endpoint.
3. Apply strict allowlist and credential rules.
4. Validate with browser-based and proxy-based test cases.
5. Roll out gradually and monitor for application regressions.
