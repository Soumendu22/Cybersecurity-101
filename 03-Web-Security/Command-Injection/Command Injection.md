# Command Injection

## Overview

Command Injection occurs when untrusted input is passed to system shell commands, allowing attackers to execute arbitrary OS commands.

---

## Typical Vulnerable Pattern

- App builds shell command with user input
- Input is interpreted by shell metacharacters

Example dangerous characters:

- `;` `&&` `||` `|` `` ` `` `$()`

---

## Impact

- Remote code execution
- Data theft and file modification
- Service disruption
- Full host compromise depending on privileges

---

## Prevention

1. Avoid shell invocation whenever possible.
2. Use safe APIs with argument arrays instead of shell strings.
3. Enforce strict allowlist validation.
4. Escape and quote defensively where shell use is unavoidable.
5. Run application with least privilege and containment.

---

## Defense-in-Depth

- Sandboxing/containers
- AppArmor/SELinux policy
- Restricted execution accounts
- Runtime monitoring for suspicious child processes

---

## Testing Checklist

- Are user inputs included in OS command strings?
- Can metacharacters alter command behavior?
- Are API alternatives available without shell?
- Does command output leak sensitive system data?
- What privilege context executes commands?

---

## Practice Tasks

1. Identify and exploit command injection in a lab endpoint.
2. Refactor vulnerable shell execution to safe argument-based calls.
3. Add strict allowlist validators for command parameters.
4. Restrict runtime account permissions and retest impact.
5. Add monitoring for suspicious process spawning.

---

## Common Root Causes in Code Reviews

- String concatenation into shell command lines
- Using helper wrappers that silently invoke shell mode
- Reusing user input for both display and execution logic
- Missing separation between command and argument boundaries

---

## Safe Implementation Pattern

1. Prefer built-in language APIs over shell commands.
2. If external process needed, pass arguments as array/list.
3. Disallow dynamic command selection from user input.
4. Validate each argument against strict allowlists.
5. Enforce timeouts and output size limits.

---

## Environment Hardening

- Run service as non-privileged account.
- Remove unnecessary binaries from runtime image.
- Apply syscall and process execution restrictions.
- Use read-only filesystems where feasible.

---

## Detection and Telemetry

- Monitor unexpected child process trees from web workers.
- Alert on suspicious command-line patterns.
- Correlate process activity with incoming request metadata.
- Track spikes in command execution failures.

---

## Incident Response

1. Isolate affected host/container.
2. Capture process, network, and filesystem evidence.
3. Rotate secrets accessible to compromised runtime.
4. Patch vulnerable code path and redeploy.
5. Hunt for persistence mechanisms and lateral movement.
