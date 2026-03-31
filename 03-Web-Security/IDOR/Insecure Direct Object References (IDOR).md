# Insecure Direct Object Reference (IDOR)

## Overview

IDOR occurs when an application exposes object identifiers (numeric IDs, UUIDs, filenames) without enforcing authorization checks per object.

---

## Typical Pattern

User accesses:

- `/api/orders/1001`

Attacker changes ID:

- `/api/orders/1002`

If server only checks authentication (not ownership/permissions), unauthorized access occurs.

---

## High-Risk Areas

- User profiles and records
- Invoices/orders
- Support tickets
- File download endpoints
- Admin function APIs

---

## Root Causes

- Missing object-level authorization
- Trusting client-supplied identifiers
- Assuming unguessable IDs are enough
- Inconsistent checks across microservices/endpoints

---

## Prevention

1. Enforce authorization server-side for every object access.
2. Use policy checks based on user role + resource ownership.
3. Avoid exposing direct internal identifiers where possible.
4. Use indirect references/tokenized resource mapping when suitable.
5. Add centralized authorization middleware and test coverage.

---

## Testing Workflow

1. Authenticate as low-privilege user.
2. Identify object references in URL/body/API calls.
3. Iterate IDs/UUIDs and observe response differences.
4. Test read, update, and delete operations.
5. Confirm access control failures and business impact.

---

## Practice Tasks

1. Build a matrix of endpoints requiring object-level checks.
2. Test horizontal and vertical privilege boundaries.
3. Add policy-based access control and regression tests.
4. Validate authorization consistency across all HTTP methods.
5. Review logs for suspicious object access patterns.

---

## Horizontal vs Vertical Access Control Failures

- Horizontal: user accesses another user's resources at same privilege level.
- Vertical: lower privilege user reaches admin-only resources.

IDOR often starts as horizontal but can chain into vertical privilege issues.

---

## Authorization Design Pattern

1. Authenticate user identity and role.
2. Load target object securely.
3. Evaluate policy: ownership, tenant boundary, role scope.
4. Deny by default with consistent error handling.
5. Log decision outcome for audit.

---

## API and Microservice Challenges

- Inconsistent checks across service boundaries
- Caching layers returning data without policy re-check
- Background workers processing object operations without ownership validation

Shared authorization libraries and policy engines reduce drift.

---

## Detection and Monitoring

- Alert on sequential object ID probing behavior.
- Monitor repeated 403/404 patterns per account/IP.
- Track cross-tenant object access attempts.
- Include object owner and requester identifiers in audit logs.

---

## Remediation Playbook

1. Patch missing object-level checks centrally.
2. Audit all endpoints for similar authorization gaps.
3. Review logs for prior unauthorized access.
4. Notify impacted parties if data exposure occurred.
5. Add automated access-control tests in CI/CD.
