# Reloader

**Reloader** (by Stakater) automatically **restarts Kubernetes Deployments** when their referenced `Secret` or `ConfigMap` changes.

It ensures that:
- Applications always use the latest credentials.
- Updates propagated by ESO or Reflector trigger automatic rollouts.
- The GitOps flow remains declarative and auditable.

---

## ⚙️ Example Annotation

```yaml
metadata:
  annotations:
    secret.reloader.stakater.com/reload: "db-credentials"
```

When the Secret `db-credentials` is updated, Reloader triggers a new Deployment rollout.

---

## 🔄 Combined Lifecycle

```
GCPSM → ESO (infra) → Reflector → Secret (app ns) → Reloader → Pod restart
```

This guarantees that applications always operate with the latest, synchronized credentials.

---

## ✅ Benefits

| Feature | Description |
|----------|-------------|
| 🔁 Auto-rollout | Redeploys apps when secrets change. |
| 🧠 Simple Integration | Just annotations — no extra controller logic. |
| 🧩 Compatible | Works seamlessly with ESO + Reflector. |

---

**Next:** [CSI Secret Store →](csi-secret-store.md)
