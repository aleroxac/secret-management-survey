# SOPS (Secrets OPerationS)

**SOPS** is a tool for **encrypting and decrypting files** (e.g., YAML manifests) using PGP, AWS KMS, GCP KMS, or Vault keys.

It’s widely adopted for **GitOps-based secret encryption**.

---

## 🧰 Example Usage

```bash
# Encrypt a secret
sops --encrypt secret.yaml > secret.enc.yaml

# Decrypt it back
sops --decrypt secret.enc.yaml > secret.yaml
```

---

## ✅ Pros

| Advantage | Description |
|------------|-------------|
| 🔐 Secure Storage | Secrets can be safely committed to Git. |
| 🧩 Flexible | Works with GPG, AWS, GCP, and Vault keys. |
| 🕵️ Auditable | Full version history in Git. |

---

## ❌ Cons

| Limitation | Description |
|-------------|-------------|
| 🧱 Duplication | Every secret update requires manual re-encryption. |
| 🔄 No runtime sync | Rotation requires commit & redeploy. |
| ⚙️ Operational overhead | Scaling across many apps is cumbersome. |

---

**Next:** [Sealed Secrets →](sealed-secrets.md)
