# Reflector

The **Reflector** (by EmberStack) automatically **replicates Secrets and ConfigMaps across namespaces**.

It enables:
- Centralized secret creation (e.g., in an `infra` namespace).
- Automatic propagation to multiple application namespaces.
- Continuous synchronization and updates between namespaces.

---

## 🧩 Why It Matters

In Kubernetes, a `Deployment` cannot reference a `Secret` or `ConfigMap` from another namespace.  
This isolation creates friction when multiple apps need the same credentials (e.g., shared databases or APIs).

The Reflector solves this by **automatically duplicating** resources with consistent content across namespaces, while maintaining sync.

---

## 🧱 Example Configuration

```yaml
metadata:
  annotations:
    reflector.v1.k8s.emberstack.com/reflection-allowed: "true"
    reflector.v1.k8s.emberstack.com/reflection-auto-enabled: "true"
    reflector.v1.k8s.emberstack.com/reflection-allowed-namespaces: ".*"
```

With these annotations:
- The source `Secret` will be replicated to all namespaces matching the regex.
- When the source updates, all replicas update automatically.

---

## ✅ Benefits

| Feature | Description |
|----------|-------------|
| 🔁 Automated Sync | Reflects updates in real time. |
| 🧩 Multi-tenant Support | Each namespace receives its own copy. |
| 🔒 Isolation | No need for risky cross-namespace references. |
| ⚙️ Compatible | Works with ESO, Reloader, and ArgoCD. |

---

## 🔗 Integration Example

```
GCPSM → ESO (infra ns) → Reflector → App Namespace Secret → Reloader → Deployment Rollout
```

---

**Next:** [Reloader →](reloader.md)
