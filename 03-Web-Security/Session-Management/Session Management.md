# Session Management Security

## Overview

After authentication, sessions maintain user state. Weak session design can allow attackers to hijack or fix sessions and impersonate users.

---

## Session Token Requirements

A secure session identifier must be:

- Unpredictable (high entropy)
- Unique per session
- Short-lived or actively rotated
- Transmitted only over HTTPS

---

## Cookie Security Flags

Use secure cookie attributes:

- `HttpOnly`: blocks JavaScript access to cookie
- `Secure`: send cookie only over HTTPS
- `SameSite`: mitigates CSRF (`Lax` or `Strict` where feasible)

Example:

```http
Set-Cookie: session=...; HttpOnly; Secure; SameSite=Lax; Path=/
```

---

## Session Lifecycle Controls

- Regenerate session ID after login and privilege changes
- Invalidate session on logout server-side
- Enforce idle and absolute timeouts
- Revoke all sessions after password reset or account compromise

---

## Common Session Vulnerabilities

- Session fixation (ID not rotated on login)
- Session IDs in URL parameters
- Missing timeout or long-lived sessions
- Weak random token generation
- Insecure storage in localStorage for sensitive tokens

---

## Session Hijacking Vectors

- XSS stealing tokens (unless HttpOnly)
- MITM on non-HTTPS traffic
- Token leakage via referrer logs
- Browser extension or endpoint compromise

---

## Server-Side Session Design

- Store session state server-side with token reference
- Bind session to risk signals (IP/device heuristics) carefully
- Keep centralized session store for distributed systems
- Use revocation lists for stateless token architectures

---

## JWT Considerations

If using JWT for sessions:

- Keep expiration short
- Validate signature, issuer, audience, and algorithm strictly
- Avoid storing sensitive data in token payload
- Use refresh-token rotation and revocation strategy

---

## Testing Checklist

- Is session ID rotated on login?
- Can old session remain valid after logout?
- Are cookie flags configured correctly?
- Does timeout policy actually enforce logout?
- Can session ID be brute-forced or predicted?

---

## Practice Tasks

1. Inspect cookies in browser devtools and validate flags.
2. Attempt session fixation in a lab app.
3. Test idle timeout and absolute timeout behavior.
4. Verify session invalidation after password change.
5. Compare server-side sessions vs JWT session models.

---

## Session Architecture Tradeoffs

Server-side sessions:

- easier revocation and central control
- requires shared storage in distributed systems

Token-based sessions:

- stateless scaling advantages
- revocation and replay controls require careful design

---

## Token Rotation and Replay Defense

- Rotate refresh tokens on every use.
- Detect reuse of rotated refresh token as compromise signal.
- Bind session tokens to risk context where feasible.
- Revoke full token family after suspicious reuse.

---

## Cross-Device Session Management

- Expose active session inventory to users.
- Support per-device sign-out and global sign-out.
- Alert users for new device/session creation.
- Force re-authentication for critical account changes.

---

## Monitoring and Detection

- Detect token reuse anomalies from different geographies.
- Alert on sudden session creation spikes.
- Track session age outliers and missing timeout enforcement.
- Correlate session events with authentication logs.

---

## Incident Response Steps

1. Revoke sessions and token sets for impacted accounts.
2. Investigate source of token leakage (XSS, logs, proxy, endpoint).
3. Rotate signing keys/secrets if systemic risk exists.
4. Harden cookie and timeout configuration.
5. Add regression tests for fixation/hijacking scenarios.
