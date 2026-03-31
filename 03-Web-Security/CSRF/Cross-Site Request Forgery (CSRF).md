# Cross-Site Request Forgery (CSRF)

## Overview

CSRF tricks an authenticated victim's browser into sending unintended state-changing requests to a target application.

It relies on automatic credential inclusion (cookies, HTTP auth, client certs).

---

## Typical Attack Conditions

- Victim is authenticated to target app
- Browser auto-sends credentials
- Endpoint lacks CSRF defenses
- Attacker can cause victim to submit crafted request

---

## Common Targets

- Email or password change
- Payment/address updates
- Account privilege settings
- API state-change endpoints

---

## Defense Mechanisms

### Anti-CSRF Tokens

- Unique per session/request
- Unpredictable
- Verified server-side
- Bound to user session context

### SameSite Cookies

- `SameSite=Lax` or `Strict` reduces cross-site cookie sending
- Not a complete replacement for token validation

### Origin/Referer Validation

- Validate expected origin for sensitive operations
- Handle edge cases carefully (privacy tools, proxies)

### Re-authentication for High-Risk Actions

Require password/MFA confirmation before sensitive changes.

---

## Common Mistakes

- Token present but not validated
- Token reused indefinitely without rotation strategy
- Token accepted in GET endpoints
- JSON/API endpoints assumed safe without CSRF checks

---

## Testing Checklist

- Can sensitive actions be triggered from external site?
- Are anti-CSRF tokens required and validated?
- Is SameSite configured for session cookies?
- Are dangerous operations exposed via GET?
- Can token be guessed/replayed across users?

---

## Practice Tasks

1. Build a CSRF proof-of-concept for a lab app.
2. Implement synchronized token pattern and verify rejection paths.
3. Test SameSite cookie behavior across browser contexts.
4. Add origin checks to critical endpoints.
5. Validate protection coverage for REST and GraphQL endpoints.

---

## CSRF in API-Heavy Applications

CSRF still applies to APIs when browsers automatically send credentials (cookies/session-based auth).

Risk is lower for properly scoped bearer tokens sent manually by frontend code, but mixed auth models can reintroduce exposure.

---

## Token Pattern Options

- Synchronizer token pattern (server-stored expected token)
- Double-submit cookie pattern (with robust signing/integrity)
- Per-request tokens for highly sensitive operations

Choose pattern based on architecture and operational simplicity.

---

## Browser and UX Considerations

- `SameSite=Lax` helps for standard navigation but does not replace token checks.
- Legacy browser behavior and embedded flows may differ.
- Cross-origin integrations should be reviewed for side effects.

---

## Detection and Monitoring

- Log CSRF validation failures with request metadata.
- Monitor spikes in rejected state-changing requests.
- Correlate failed token checks with suspicious referer/origin patterns.
- Alert on state-changing GET requests in production logs.

---

## Remediation Workflow

1. Identify all state-changing endpoints.
2. Enforce token + origin validation consistently.
3. Set strict cookie attributes and review exceptions.
4. Add automated CSRF tests for all sensitive operations.
5. Reassess whenever auth/session architecture changes.
