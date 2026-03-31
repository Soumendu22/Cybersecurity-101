# Server-Side Template Injection (SSTI)

## Overview

SSTI occurs when untrusted input is interpreted by a server-side template engine, potentially allowing arbitrary code execution or data disclosure.

---

## Typical Vulnerable Pattern

- User input directly passed into template rendering context
- Dynamic template creation from request parameters
- Unsafe expression evaluation in templates

---

## Impact

- Remote code execution
- Access to internal objects/configuration
- Secret leakage
- Full server compromise in severe cases

---

## Prevention

1. Never render raw user input as template code.
2. Use strict context binding and auto-escaping.
3. Disable dangerous template engine features where possible.
4. Apply sandboxing for template evaluation.
5. Keep template engines patched and configured securely.

---

## Testing Checklist

- Are user-controlled values interpreted as expressions?
- Can template syntax trigger object introspection?
- Is sensitive runtime context exposed in rendered output?
- Are risky debug/template functions enabled?

---

## Practice Tasks

1. Identify SSTI in a lab app and validate exploitability safely.
2. Refactor dynamic template rendering to static templates.
3. Harden template engine settings and sandbox policies.
4. Add tests to ensure user input is treated as data only.
5. Review template code paths for server-side expression parsing.

---

## High-Risk Template Engines and Behaviors

Different stacks have different dangerous primitives:

- Python engines (for example Jinja2) with unsafe expression evaluation
- Java template engines exposing class loader or runtime objects
- JavaScript template engines with direct code execution helpers

Risk increases when templates can access filesystem, process runtime, or environment variables.

---

## Secure Architecture Guidance

- Keep template files static and version-controlled.
- Separate template selection logic from user input.
- Pass only minimal rendering context data.
- Disable debug helpers and expression evaluators in production.
- Apply strict code review for any dynamic rendering path.

---

## Detection Clues During Assessment

- Unexpected expression evaluation in page output
- Server errors exposing template engine internals
- Ability to enumerate object properties from template context
- Template syntax accepted in user-controllable fields

---

## Remediation Workflow

1. Inventory all rendering entry points.
2. Remove dynamic template compilation from request data.
3. Replace dangerous features with safe placeholders/helpers.
4. Add security unit tests for expression execution attempts.
5. Re-test after deployment and monitor templating errors.

---

## Blue-Team Monitoring Ideas

- Alert on unusual template parsing errors.
- Monitor sudden spikes in 500 responses on render routes.
- Track suspicious characters in high-risk parameters.
- Correlate web logs with process anomalies on app hosts.

