# Authentication Security

## Overview

Authentication verifies identity before granting access. Weak authentication design leads to account takeover, privilege abuse, and lateral movement.

---

## Authentication Factors

- Something you know: password, PIN
- Something you have: TOTP app, hardware token
- Something you are: biometrics

Best practice: multi-factor authentication (MFA) for admin and sensitive operations.

---

## Common Authentication Flaws

- Weak password policy (short, reused, predictable passwords)
- No rate limiting or lockout controls
- Username enumeration via login/forgot-password responses
- Insecure password reset flow
- Missing MFA on critical users
- Default credentials not changed

---

## Password Storage

Passwords must be stored as salted adaptive hashes, not plaintext.

Recommended algorithms:

- Argon2id (preferred)
- bcrypt
- scrypt

Avoid:

- MD5
- SHA-1
- unsalted SHA-256 for passwords

---

## Secure Login Flow

1. Validate input format.
2. Retrieve account by normalized identifier.
3. Compare submitted secret using constant-time verification.
4. Apply failure counters and rate limits.
5. Issue secure session token only after successful auth.
6. Log suspicious and failed attempts.

---

## Brute-Force and Credential Stuffing Defense

- Per-account and per-IP rate limiting
- Temporary lockouts with safe recovery path
- CAPTCHA after repeated failures
- Password breach checks against known leaked sets
- MFA and anomaly-based checks (new device/location)

---

## Account Recovery Security

- Use single-use, short-expiry reset tokens
- Invalidate previous reset tokens on new request
- Never reveal whether email exists
- Require re-authentication for high-risk profile changes

---

## Authentication Testing Checklist

- Can invalid and valid usernames be distinguished?
- Is there effective brute-force throttling?
- Are default credentials accepted?
- Are session tokens rotated after login?
- Is MFA bypass possible in alternate endpoints?
- Can password reset token be predicted/reused?

---

## Secure Design Recommendations

- Centralized identity provider for enterprise apps
- Risk-based authentication for unusual behavior
- Mandatory MFA for privileged users
- Password managers and long passphrases
- Full login audit trail with alerting

---

## Practice Tasks

1. Build a test matrix for login, lockout, and recovery edge cases.
2. Simulate credential stuffing in a lab and verify rate-limit controls.
3. Review password hashing configuration in a demo app.
4. Test if login errors leak username existence.
5. Document threat scenarios and mitigations for auth endpoints.

---

## Modern Authentication Architecture

- Centralized identity provider (OIDC/SAML) for consistency
- Short-lived access tokens with refresh-token rotation
- Device/session risk scoring for adaptive challenges
- Service-to-service authentication separate from user authentication

---

## MFA Implementation Pitfalls

- Allowing fallback to weak channels without risk checks
- Missing MFA requirement on API and mobile flows
- MFA skipped on high-risk profile/account operations
- Recovery mechanisms that bypass MFA controls

---

## Logging and Detection Strategy

- Track failed logins by user, IP, ASN, and device fingerprint
- Alert on impossible travel and sudden geo/device changes
- Detect password spraying patterns across many accounts
- Log password reset and MFA enrollment events with high fidelity

---

## Secure Account Lifecycle

1. Provision accounts with minimal default privileges.
2. Verify identities for sensitive role assignments.
3. Enforce periodic credential hygiene and MFA checks.
4. Deprovision quickly on role change/offboarding.
5. Invalidate sessions and tokens on lifecycle events.

---

## Incident Response for Auth Abuse

1. Triage suspicious login activity and affected accounts.
2. Force credential reset and session revocation.
3. Review privilege changes during compromise window.
4. Tune controls (rate limits, MFA policy, anomaly thresholds).
5. Document root cause and regression controls.

