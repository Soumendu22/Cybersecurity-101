# SQL Injection (SQLi)

## Overview

SQL Injection happens when untrusted input is concatenated into SQL queries, allowing attackers to alter query logic.

---

## Common SQLi Types

- In-band SQLi (error-based, union-based)
- Blind SQLi (boolean-based, time-based)
- Second-order SQLi (payload stored and executed later)

---

## Typical Vulnerable Pattern

Unsafe query construction:

```sql
SELECT * FROM users WHERE username = '" + input + "' AND password = '" + pass + "'
```

---

## Impact

- Authentication bypass
- Data exfiltration
- Data tampering/deletion
- Database admin access
- OS-level compromise in severe DB misconfigurations

---

## Prevention

1. Use parameterized queries/prepared statements.
2. Avoid dynamic SQL where possible.
3. Enforce input validation (allowlist where practical).
4. Apply least privilege DB accounts.
5. Hide detailed SQL errors from users.
6. Monitor anomalous query behavior.

---

## Detection Clues

- SQL error messages in responses
- Time delays on crafted payloads
- Response changes with boolean conditions
- Unexpected data returned via UNION tests

---

## Testing Workflow

1. Identify input vectors in query, body, headers.
2. Probe for error leakage and behavior differences.
3. Test boolean and time-based payload logic safely.
4. Confirm exploitability with minimal-impact methods.
5. Document affected query paths and remediation.

---

## Tooling

- Manual testing through intercepting proxy
- sqlmap (authorized use only)

---

## Practice Tasks

1. Exploit and fix SQLi in a vulnerable lab app.
2. Convert raw string queries to prepared statements.
3. Apply DB least privilege and verify operation constraints.
4. Add automated security tests for SQLi regressions.
5. Build alerting for suspicious query patterns.

---

## SQLi in Modern Architectures

SQLi still appears in:

- legacy code paths inside modern apps
- ORMs when raw query interfaces are used unsafely
- reporting/search features with dynamic filter construction
- migration scripts and internal admin tooling

---

## Database-Specific Risk Considerations

- Function abuse differs across MySQL, PostgreSQL, MSSQL, Oracle.
- Privileged DB roles increase blast radius significantly.
- File read/write and extension features can escalate impact.

Use narrowly scoped service accounts per application component.

---

## Secure Query Construction Rules

1. Parameterize every user-controlled value.
2. For dynamic identifiers (table/order fields), use strict allowlists.
3. Keep query templates static where possible.
4. Separate read-only and write-capable DB credentials.
5. Apply query timeout/resource limits for resilience.

---

## Detection and Monitoring

- Alert on repeated SQL syntax errors from application layer.
- Detect unusual time-based query latency patterns.
- Monitor anomalous query volume and schema access.
- Correlate WAF/proxy anomalies with database logs.

---

## Remediation Workflow

1. Patch vulnerable query path with prepared statements.
2. Rotate credentials if compromise suspected.
3. Review logs for unauthorized data access.
4. Add regression tests for injection payload classes.
5. Include secure query rules in code review checklist.
