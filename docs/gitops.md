# GitOps Approaches to Secret Management

GitOps-oriented encryption keeps all configurations, including secrets, under version control.  
The two main tools in this category are **SOPS** and **Sealed Secrets**.

They prioritize:
- Declarative infrastructure.
- Code review and auditability.
- KMS-backed encryption.

---

### Advantages
- Centralized GitOps workflows.
- Version-controlled secrets.
- Integration with CI/CD pipelines.

### Disadvantages
- Harder to rotate shared credentials.
- No real-time sync from providers.
- Secrets are decrypted at apply-time — not runtime.

---

📘 Dive deeper:
- [SOPS](soaps.md)
- [Sealed Secrets](sealed-secrets.md)

➡️ Continue to [ESO — External Secrets Operator](eso.md)
