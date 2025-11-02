# External Secrets Operator (ESO)

The **External Secrets Operator (ESO)** bridges external secret stores (e.g., GCP Secret Manager, AWS SM, HashiCorp Vault) and Kubernetes.

It **automates synchronization** — no plaintext in Git, no manual rotation.

---

## Key Features
- Fetch secrets from external providers.
- Sync to Kubernetes `Secret` objects.
- Support JSON and key-value data.
- Compatible with GitOps tools (ArgoCD, Flux).
- Integrates with Reflector and Reloader for full automation.

---

## Why It Matters
ESO shifts the security boundary:
> from “encrypting YAML in Git” → to “syncing runtime secrets from a secure source”.

---

## Architecture
```
Cloud Secret Manager → ESO → K8s Secret → App Deployment
```

---

## Future Enhancements
Planned extensions include support for a `secretDataType` field:
- `json`: current ESO default flow.
- `kv`: converts key=value format to JSON before sync.
- `encrypt`: creates encrypted Kubernetes Secrets and injects sidecar containers for runtime decryption.

---

**Next:** [Reflector →](reflector.md)
