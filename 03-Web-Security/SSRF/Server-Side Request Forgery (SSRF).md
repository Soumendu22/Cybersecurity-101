# Server-Side Request Forgery (SSRF)

## Overview

SSRF allows attackers to make the server send requests to unintended destinations, including internal networks and cloud metadata endpoints.

---

## Typical Vulnerable Features

- URL preview/fetch endpoints
- Webhook delivery testing
- Import-from-URL functionality
- Server-side image/document fetchers

---

## Impact

- Internal service discovery and access
- Cloud credential theft from metadata services
- Bypass of network segmentation
- Pivot to internal admin panels

---

## High-Risk Targets

- `127.0.0.1` and localhost-bound services
- RFC1918 private ranges
- Link-local addresses
- Cloud metadata endpoints (for example IMDS)

---

## Prevention

1. Strict allowlist of approved outbound hosts/schemes.
2. Resolve and validate DNS/IP after redirects.
3. Block internal, loopback, and link-local destinations.
4. Disable unsupported URL schemes (`file://`, `gopher://`, etc.).
5. Enforce outbound network egress controls.
6. Use metadata service hardening in cloud environments.

---

## Testing Checklist

- Can requests target localhost or internal IPs?
- Are redirects abused to reach blocked targets?
- Are alternative IP formats accepted?
- Are non-HTTP schemes blocked?
- Is response content from internal systems exposed?

---

## Practice Tasks

1. Build SSRF test cases for URL fetch endpoints.
2. Implement host allowlist + DNS rebinding safeguards.
3. Add network egress policy denying internal ranges.
4. Test cloud metadata endpoint exposure in lab.
5. Document SSRF controls in architecture security standards.

---

## SSRF Evasion Techniques to Defend Against

- Alternative IP notations (decimal, octal, hex forms)
- DNS rebinding between validation and request execution
- Redirect chains to internal destinations
- IPv6 loopback and link-local variants
- Mixed scheme abuse through parser quirks

---

## Cloud-Specific Risk Notes

- Metadata service endpoints can expose temporary credentials.
- Containerized workloads may expose internal control plane APIs.
- Service mesh and internal admin endpoints are common pivot targets.

Cloud hardening should include metadata protections, IMDS safeguards, and strict egress controls.

---

## Secure Fetch Service Pattern

1. Parse URL with hardened parser.
2. Enforce allowed schemes and ports.
3. Resolve DNS and validate final IP against blocked ranges.
4. Disable automatic redirects or re-validate each hop.
5. Apply response size/time limits.
6. Return only sanitized response metadata where possible.

---

## Monitoring and Detection

- Alert on outbound requests to internal ranges from web tier.
- Monitor denied SSRF policy events with request context.
- Track spikes in URL fetch endpoint usage.
- Correlate SSRF attempts with auth anomalies and recon activity.

---

## Incident Response Workflow

1. Block affected fetch endpoints or enforce emergency deny policy.
2. Identify whether internal resources were reached.
3. Rotate potentially exposed credentials/tokens.
4. Review outbound logs and cloud audit trails.
5. Add regression tests for known bypass vectors.
