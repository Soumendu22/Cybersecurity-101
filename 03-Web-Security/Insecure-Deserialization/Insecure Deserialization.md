# Insecure Deserialization

## Overview

Insecure deserialization happens when untrusted serialized data is deserialized into objects without integrity validation, allowing object injection and potentially code execution.

---

## Common Risk Scenarios

- Session/state objects in cookies
- Queue messages from untrusted sources
- API parameters containing serialized blobs
- Legacy binary serialization frameworks

---

## Impact

- Remote code execution
- Authentication bypass
- Privilege escalation
- Data tampering and logic abuse

---

## Prevention

1. Avoid native object deserialization for untrusted data.
2. Use simple data formats with strict schemas.
3. Verify integrity/signatures of serialized payloads.
4. Enforce allowlists for accepted types/classes.
5. Isolate deserialization components with least privilege.

---

## Detection and Testing

- Identify endpoints accepting serialized content.
- Check if payload tampering changes behavior.
- Probe type confusion/object gadget execution in labs only.
- Validate signing/verification controls are mandatory.

---

## Practice Tasks

1. Inventory all serialization/deserialization points in an app.
2. Replace unsafe object deserialization with schema-validated JSON.
3. Implement and verify signed payload handling.
4. Add allowlisted type enforcement and tests.
5. Build incident playbook for suspected deserialization abuse.

---

## Typical Root Causes

- Trusting client-side state blobs as authoritative
- Missing cryptographic integrity on serialized content
- Legacy framework defaults allowing polymorphic type loading
- Deserializing data before authentication/authorization checks

---

## High-Risk Technical Patterns

- Native object streams over HTTP cookies or hidden fields
- Message broker consumers accepting untrusted serialized payloads
- Caches/session stores that deserialize attacker-reachable data
- Language runtimes with known gadget chains in common libraries

---

## Secure Migration Strategy

1. Replace binary object serialization with JSON or protobuf schemas.
2. Validate structure with strict schema validators.
3. Reject unknown fields/types by default.
4. Sign payloads where integrity is required.
5. Keep parser and dependency stack patched.

---

## Detection and Monitoring

- Alert on deserialization exceptions and unusual type resolution errors.
- Track spikes in request failures on state/session endpoints.
- Log signature verification failures with source metadata.
- Monitor for post-deserialization anomalous behavior.

---

## Incident Response Considerations

1. Determine if untrusted payload reached deserialization routine.
2. Identify possible gadget execution surface.
3. Rotate session secrets and invalidate active sessions.
4. Patch framework/library and disable risky features.
5. Perform retrospective log and integrity review.
