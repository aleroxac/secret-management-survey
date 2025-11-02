# RBAC and IAM Integration

Secure secret management depends on robust **Role-Based Access Control (RBAC)** and **cloud IAM integration**.

---

## 🧩 Kubernetes RBAC

Use RBAC to limit which service accounts and namespaces can **view**, **list**, or **update** secrets.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "list"]
```

```yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: read-secrets
subjects:
- kind: ServiceAccount
  name: app-sa
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## ☁️ Cloud IAM Integration

| Cloud | Mechanism | Purpose |
|--------|------------|----------|
| **GCP** | Workload Identity Federation | Map K8s SA → GCP SA for secret access. |
| **AWS** | IRSA (IAM Role for Service Accounts) | Bind IAM roles directly to pods. |
| **Azure** | Managed Identity | Auto-inject Azure credentials securely. |

---

## 🔐 Combined Workflow

```
K8s SA → Cloud IAM Role → Secret Manager Access → ESO Sync → App Pod
```

---

**Next:** [Compliance →](compliance.md)
