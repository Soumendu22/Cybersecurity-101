# HTTP Protocol Security

## Overview

HTTP is the core protocol of web communication. Understanding methods, headers, status codes, and message structure is essential for web security testing and defense.

---

## Request Structure

A request contains:

- Request line: method, path, version
- Headers
- Optional body

Example:

```http
POST /login HTTP/1.1
Host: app.local
Content-Type: application/json

{"username":"sam","password":"test"}
```

---

## Response Structure

A response contains:

- Status line
- Headers
- Optional body

Example:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{"result":"ok"}
```

---

## Important HTTP Methods

- `GET`: retrieve resource (should be safe/idempotent)
- `POST`: create/process data
- `PUT`: replace resource
- `PATCH`: partial update
- `DELETE`: remove resource
- `OPTIONS`: capability info

Security note: method confusion and missing access checks can expose dangerous operations.

---

## Security-Relevant Headers

Request headers:

- `Authorization`
- `Cookie`
- `Origin`
- `Referer`

Response headers:

- `Set-Cookie`
- `Content-Security-Policy`
- `X-Frame-Options`
- `X-Content-Type-Options`
- `Strict-Transport-Security`

---

## Status Codes and Security Signals

- `200`: success
- `301/302`: redirect behavior
- `400`: malformed request
- `401`: unauthenticated
- `403`: unauthorized
- `404`: not found
- `429`: rate limit
- `500`: server error (avoid verbose internals)

---

## HTTP/HTTPS Security

HTTPS provides confidentiality and integrity through TLS.

Key controls:

- force HTTPS
- enable HSTS
- disable weak TLS versions/ciphers
- use trusted certificates and proper hostname validation

---

## Common HTTP Attacks

- Request smuggling
- Host header injection
- Cache poisoning
- Header injection/response splitting
- Verb tampering

---

## CORS Security Basics

CORS controls cross-origin browser requests.

Misconfigurations include:

- wildcard origin with credentials
- reflecting arbitrary origins
- trusting null origin in risky contexts

---

## Testing Checklist

- Are sensitive endpoints exposed with unsafe methods?
- Are security headers present and correctly configured?
- Is HTTPS enforced for all pages and APIs?
- Are verbose error details leaked in responses?
- Is CORS policy tightly scoped?

---

## Practice Tasks

1. Capture a full login request/response cycle with a proxy tool.
2. Map all HTTP methods accepted by each endpoint.
3. Audit response security headers and identify missing controls.
4. Validate redirect logic and open redirect edge cases.
5. Test CORS behavior for credentialed cross-origin requests.

---

## Reverse Proxy and CDN Security Considerations

- Enforce consistent header policy at edge and origin.
- Prevent header spoofing for client IP/origin metadata.
- Validate trusted proxy chain configuration.
- Ensure cache keys include security-relevant variance.

Misaligned proxy/origin behavior can create hidden vulnerabilities.

---

## HTTP Request Smuggling Basics

Smuggling risk increases when front-end and back-end parse request boundaries differently.

Key controls:

- normalize transfer encoding behavior
- reject ambiguous/invalid message framing
- keep edge and origin parser behavior aligned

---

## Caching and Sensitive Data

- Use correct `Cache-Control` for authenticated responses.
- Avoid caching personalized API responses in shared caches.
- Review `Vary` headers to prevent cross-user cache confusion.
- Prevent cache poisoning through strict header normalization.

---

## API Security Header Baseline

- `Strict-Transport-Security`
- `Content-Security-Policy` (where browser-rendered)
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy`
- `Permissions-Policy`

Apply baseline consistently across success and error responses.

---

## Operational Monitoring

- Alert on spikes in `4xx/5xx` by route and source.
- Detect unusual method usage patterns.
- Track header anomalies and malformed request rates.
- Correlate edge and application logs for protocol abuse.
