# XML External Entity (XXE)

## Overview

XXE arises when XML parsers process external entities from untrusted XML input, potentially allowing file disclosure, SSRF, and denial of service.

---

## Typical Conditions

- XML input accepted from user/integration
- DTD/entity processing enabled
- External entity resolution not disabled

---

## Impact

- Read local files (`/etc/passwd`)
- SSRF to internal services
- Out-of-band data exfiltration
- Billion laughs/entity expansion DoS

---

## Prevention

1. Disable DTD and external entities in XML parser config.
2. Prefer safe data formats like JSON when possible.
3. Validate and sanitize XML inputs strictly.
4. Use updated secure parser libraries.
5. Isolate parsing components from sensitive network/filesystem access.

---

## Testing Checklist

- Does parser accept DTD declarations?
- Can external entity references resolve local files?
- Can parser trigger outbound network requests?
- Is DoS possible via entity expansion?

---

## Practice Tasks

1. Test XXE payloads in a controlled lab parser endpoint.
2. Harden parser configuration and verify payload failure.
3. Validate no outbound traffic occurs during XML parsing.
4. Add automated tests for XXE and entity expansion regression.
5. Document secure XML parser baselines by language stack.

---

## Where XXE Appears in Real Systems

- SOAP-based services
- SAML/XML authentication integrations
- Office/document processing pipelines
- Legacy API integrations that still accept XML payloads

Teams often miss XXE when they rely on default parser settings.

---

## Parser Hardening Checklist

1. Disable DTD processing.
2. Disable external entity resolution.
3. Disable external parameter entities.
4. Enforce payload size and entity expansion limits.
5. Use hardened parser wrappers shared across services.

---

## Architecture-Level Mitigations

- Run parser service in isolated network segment.
- Block unnecessary outbound connections from parser hosts.
- Restrict filesystem visibility for parsing runtime.
- Add egress monitoring for unexpected DNS/HTTP traffic.

---

## Detection and Logging

- Log XML parse failures with request correlation IDs.
- Alert on DTD-related parsing errors.
- Watch for parser services calling unusual internal/external destinations.
- Correlate parsing spikes with authentication or API errors.

---

## Incident Response Steps

1. Identify affected parser endpoints and integrations.
2. Block external entity processing immediately.
3. Rotate exposed secrets if file disclosure is possible.
4. Review outbound logs for data exfiltration indicators.
5. Add long-term test coverage in CI.
