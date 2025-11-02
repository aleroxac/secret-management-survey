# Secret Management Solutions

To address these issues, two main categories of solutions emerged:

| Category | Description | Examples |
|-----------|-------------|-----------|
| **GitOps Encryption** | Secrets are stored encrypted in Git repositories. | SOPS, Sealed Secrets |
| **Runtime Sync** | Secrets are synchronized dynamically from external Secret Managers. | External Secrets Operator (ESO), CSI Secret Store |

---

## GitOps-based Encryption

- 🔒 Security through encryption (PGP/KMS/GCP).
- ✅ Great for versioning and GitOps pipelines.
- ❌ Hard to rotate secrets — updates require re-encryption and commit updates across many manifests.

[Learn more → SOPS](soaps.md) | [→ Sealed Secrets](sealed-secrets.md)

---

## Runtime-based Synchronization

- Secrets are fetched from a **trusted external manager** like GCP Secret Manager, AWS SM, or Vault.
- They are synced into Kubernetes dynamically, often with **reflectors** and **reloaders** for automatic rollout.

[Learn more → External Secrets Operator](eso.md)

---

➡️ Continue to [GitOps Approaches](gitops.md)
