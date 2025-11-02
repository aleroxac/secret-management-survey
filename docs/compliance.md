# Compliance and Governance

Compliance ensures that your secret management strategy meets organizational and legal requirements such as **SOC2**, **ISO 27001**, and **PCI-DSS**.

---

## 🧩 Core Controls

| Control | Description | Example |
|----------|--------------|----------|
| **Encryption at Rest** | Secrets must be encrypted with a KMS or equivalent. | GCP CMEK, AWS KMS |
| **Access Control** | Only authorized identities can access secrets. | RBAC + IAM policies |
| **Audit Logging** | All read and write operations must be logged. | GCP Cloud Audit Logs |
| **Rotation Policy** | Secrets must be rotated regularly. | ESO + Secret Manager |
| **Segregation of Duties** | Devs can’t decrypt production secrets. | Role separation |

---

## 🧠 Recommended Practices

- Enable **Cloud Audit Logs** for every Secret Manager API call.  
- Store decrypted secrets **only in memory**, never on disk.  
- Automate **compliance evidence collection** (access logs, rotation reports).  
- Enforce **RBAC and least privilege** across teams and clusters.  

---

**Back to:** [Conclusion →](conclusion.md)
