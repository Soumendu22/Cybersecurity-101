# Clickjacking

## Overview

Clickjacking (UI redress) tricks users into clicking hidden or disguised UI elements, often by embedding target pages in transparent iframes.

---

## Attack Scenarios

- Invisible iframe over attacker-controlled page
- Decoy button that actually triggers sensitive action
- Multi-step click flows for permission grants

---

## Impact

- Unauthorized state-changing actions
- Privacy/permission abuse (camera/mic)
- Account misconfiguration via forced clicks

---

## Primary Defenses

### Frame Blocking Headers

Use one or both (CSP preferred modern control):

```http
Content-Security-Policy: frame-ancestors 'none'
X-Frame-Options: DENY
```

Alternative for trusted embedding use cases:

```http
Content-Security-Policy: frame-ancestors 'self' https://trusted.example
```

### Sensitive Action Confirmation

- Re-auth prompts
- Step-up MFA
- Explicit confirmation dialogs for destructive actions

---

## Testing Checklist

- Can pages be embedded in external origins?
- Are frame protections present on all sensitive routes?
- Do legacy endpoints miss headers?
- Can user interaction still be forced via UI tricks?

---

## Practice Tasks

1. Test if critical endpoints render inside an iframe.
2. Add CSP `frame-ancestors` and validate browser behavior.
3. Compare X-Frame-Options and CSP effectiveness.
4. Identify routes that require explicit user confirmation.
5. Document exceptions where framing is intentionally allowed.

---

## Where Clickjacking Still Appears

- Legacy admin consoles without frame protections
- Mixed micro-frontend stacks with inconsistent headers
- New endpoints behind old reverse proxies that drop headers

---

## Defense Layers Beyond Headers

- Re-authentication before destructive actions
- Transaction signing/confirmation for critical changes
- UX friction for risky actions (cooldown, confirmation text)
- Anti-automation checks for repeated sensitive clicks

---

## Browser and Deployment Considerations

- Prefer `Content-Security-Policy: frame-ancestors` as primary modern control.
- Keep `X-Frame-Options` for legacy compatibility where needed.
- Verify headers are not stripped by CDN/WAF/proxy layers.
- Ensure error pages and static routes also include protections.

---

## Validation Workflow

1. Enumerate all sensitive routes and response types.
2. Test framing from attacker-controlled origin.
3. Confirm both normal and error states are protected.
4. Validate partner embedding exceptions explicitly.
5. Add automated header presence checks in CI.
