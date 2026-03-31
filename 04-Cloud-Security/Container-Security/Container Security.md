# Container Security

## Overview

Container security covers image integrity, runtime protection, orchestration controls, and software supply chain hardening.

---

## Container Threats

- Vulnerable base images
- Secrets baked into image layers
- Running as root in container
- Privileged containers and host namespace exposure
- Insecure registry access
- Weak runtime monitoring

---

## Secure Image Build Practices

- Use minimal trusted base images
- Pin image versions/digests
- Remove build tools from runtime image
- Run as non-root user
- Use multi-stage builds

Example Dockerfile patterns:

```dockerfile
FROM python:3.12-slim AS runtime
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
RUN useradd -r appuser
USER appuser
CMD ["python", "app.py"]
```

---

## Image Scanning

Scan images for CVEs and policy violations before deployment.

Examples:

```bash
trivy image nginx:latest
grype nginx:latest
```

Use CI gates to block high-severity vulnerabilities unless exception approved.

---

## Registry Security

- Private registries for internal images
- Enforce image signing and provenance checks
- Restrict push/pull permissions
- Enable registry audit logging

---

## Runtime Security Controls

- Drop Linux capabilities not needed
- Use read-only root filesystem where possible
- Apply seccomp/AppArmor/SELinux policies
- Resource limits to reduce DoS impact

Docker checks:

```bash
docker ps
docker inspect <container-id>
docker exec -it <container-id> id
```

---

## Secrets in Containers

Avoid environment variables for highly sensitive long-lived secrets.

Use:

- cloud secret managers
- orchestrator secret objects with strict RBAC
- short-lived token retrieval patterns

---

## Supply Chain Security

- Generate SBOMs
- Verify signatures (for example cosign)
- Lock dependencies and verify hashes
- Scan IaC and pipeline configurations

Examples:

```bash
syft <image>
cosign verify <image-ref>
```

---

## Monitoring and Detection

- Alert on container running as root unexpectedly
- Detect privileged/hostNetwork/hostPID workloads
- Monitor exec into running containers
- Watch for unusual outbound traffic patterns

---

## Incident Response for Container Breach

1. Isolate affected workload/node.
2. Preserve image digest and runtime metadata.
3. Capture logs and process/network evidence.
4. Rebuild image from trusted source.
5. Rotate any exposed credentials.

---

## Practice Tasks

1. Build hardened Dockerfile for a sample app.
2. Integrate image scan in CI and fail on high CVEs.
3. Enforce non-root execution and capability drops.
4. Detect and remove secrets from existing images.
5. Implement signed image verification before deploy.
