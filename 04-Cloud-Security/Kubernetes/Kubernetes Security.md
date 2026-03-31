# Kubernetes Security

## Overview

Kubernetes security spans control plane hardening, RBAC, pod security, network policy, secrets management, and runtime monitoring.

---

## Key Kubernetes Attack Paths

- Overly permissive RBAC (`cluster-admin` misuse)
- Privileged pods and hostPath mounts
- Exposed dashboard/API server
- Weak network segmentation between namespaces
- Secret theft from etcd/pods
- Insecure admission and image policies

---

## Cluster Baseline Hardening

1. Enable RBAC and disable anonymous access.
2. Use separate namespaces by environment/team.
3. Restrict pod privileges with Pod Security standards.
4. Enforce image source/signature policies.
5. Enable audit logging and centralized observability.

---

## RBAC Security

Inspect access controls:

```bash
kubectl get clusterrolebindings
kubectl get rolebindings --all-namespaces
kubectl auth can-i '*' '*' --all-namespaces
```

Best practices:

- no default `cluster-admin` for app teams
- least privilege roles per namespace
- review rolebindings continuously

---

## Pod Security

High-risk settings to avoid:

- `privileged: true`
- `hostNetwork: true`
- `hostPID: true`
- writable root filesystem where unnecessary
- container running as root

Inspect pods:

```bash
kubectl get pods -A -o wide
kubectl get pod <pod> -n <ns> -o yaml
```

---

## Network Policies

Use default deny and allow explicitly per namespace/app path.

```bash
kubectl get networkpolicy -A
```

Policy goals:

- isolate workloads by function
- restrict egress to required services only
- reduce lateral movement opportunities

---

## Secrets and Config Security

- Encrypt secrets at rest
- Restrict RBAC access to secrets
- Avoid plaintext secrets in manifests and images
- Rotate secrets and service account tokens

```bash
kubectl get secrets -A
kubectl describe secret <name> -n <ns>
```

---

## Admission and Policy Enforcement

Use policy engines/admission controls:

- OPA Gatekeeper / Kyverno
- deny privileged pods
- require trusted registries
- enforce resource limits and labels

---

## Supply Chain and Image Controls

- scan images before deploy
- enforce signed images
- pin image tags to digests where practical
- block `latest` tag in production policy

---

## Monitoring and Detection

- Kubernetes audit logs
- suspicious `kubectl exec` activity
- unusual service account token usage
- unexpected new cluster role bindings

---

## Incident Response (Kubernetes)

1. Isolate namespace/workload (network policy/scale down).
2. Preserve pod logs and node artifacts.
3. Revoke compromised service account tokens.
4. Rebuild and redeploy from trusted images.
5. Re-audit RBAC and admission policy coverage.

---

## Practice Tasks

1. Audit and remove excessive RBAC permissions.
2. Apply pod security baseline policy to all namespaces.
3. Implement default deny network policy.
4. Restrict images to approved registries.
5. Simulate compromised pod and run containment workflow.
