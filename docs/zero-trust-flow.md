# Zero Trust Secret Flow

The **Zero Trust Secret Flow** enforces the principle of *"never trust, always verify"* for every access to a secret in your infrastructure.

---

## 🧩 Core Principles

| Principle | Description |
|------------|-------------|
| **Least Privilege** | Each workload can only access the secrets it truly needs. |
| **Identity-Aware Access** | Authentication through workload identity, not static credentials. |
| **Segregation of Duties** | Separate responsibility for secret creation, access, and rotation. |
| **Continuous Verification** | Every secret request must be verified by policy. |

---

## 🧱 Architecture Example

```mermaid
graph TD
  A[Workload Identity (KSA/GSA)] -->|OIDC Token| B[GCP Secret Manager]
  B -->|Scoped IAM Policy| C[ESO / CSI Driver]
  C -->|Reflect & Sync| D[Kubernetes Secret (namespace scope)]
  D -->|envFrom or volume| E[Application Pod]
```

---

## 🔒 Implementation Best Practices

- Use **Workload Identity Federation** instead of long-lived service account keys.  
- Restrict secret access per **namespace**, **label**, or **resource type**.  
- Combine ESO with **Reflector** for controlled multi-namespace propagation.  
- Audit access using **KMS logs** and **Cloud Audit Logs**.  

---

**Next:** [Secret Rotation Strategies →](secret-rotation.md)
