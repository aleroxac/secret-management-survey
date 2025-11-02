# Sealed Secrets

**Sealed Secrets** encrypts Kubernetes Secrets into “sealed” YAML manifests that can safely live in Git repositories.

A controller inside the cluster decrypts them using a private key, creating actual `Secret` objects.

---

## 🧩 Workflow Example

```bash
kubeseal --cert pub-cert.pem < secret.yaml > sealed-secret.yaml
kubectl apply -f sealed-secret.yaml
```

---

## ✅ Advantages

| Feature | Description |
|----------|-------------|
| 🔐 Secure Git Storage | Safe to commit encrypted manifests. |
| 🧩 Simple CLI | Easy encryption/decryption process. |
| 🧱 Declarative | Works seamlessly with GitOps flows. |

---

## ❌ Limitations

| Limitation | Description |
|-------------|-------------|
| 🔑 Cluster-bound Keys | Each cluster has its own keypair. |
| ⚙️ No Rotation | Secrets don’t auto-rotate. |
| 🧱 Duplication | Shared credentials must be sealed per app. |

---

## 🧠 When to Use

Sealed Secrets are ideal when:
- You want a **GitOps-native** approach with encrypted manifests.
- You manage few clusters and don’t need frequent secret rotations.
- You rely on declarative manifests and CI/CD pipelines for delivery.

However, for large-scale setups or frequent rotations, runtime-based solutions like [External Secrets Operator](eso.md) or [CSI Secret Store](csi-secret-store.md) are more suitable.

---

**Next:** [CSI Secret Store →](csi-secret-store.md)
