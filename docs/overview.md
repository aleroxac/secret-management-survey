# Secret Management Research — Overview

This research covers tools, patterns, and strategies for managing secrets in Kubernetes, focusing on:
- **Security**: encryption at rest and in transit.
- **Automation**: automatic syncing and rotation.
- **Scalability**: multi-namespace, multi-cluster environments.
- **GitOps Integration**: declarative, auditable workflows.

---

## 📚 Table of Contents

1. [Introduction](introduction.md)
2. [Problems](problems.md)
3. [Solutions Overview](solutions.md)
4. [GitOps Approaches](gitops.md)
   - [SOPS](soaps.md)
   - [Sealed Secrets](sealed-secrets.md)
5. [Runtime Operators](eso.md)
   - [Reflector](reflector.md)
   - [Reloader](reloader.md)
6. [CSI Secret Store](csi-secret-store.md)
7. [encryption-lifecycle](encryption-lifecycle.md)
8. [zero-trust-flow](zero-trust-flow.md)
9. [secret-rotation](secret-rotation.md)
10. [rbac-iam](rbac-iam.md)
11. [compliance](compliance.md)
12. [Conclusion](conclusion.md)
13. [References](references.md)

---

## 🧩 Related Demo

A working demo is included under [`/demo`](../demo):
- [RUNBOOK.md](../demo/RUNBOOK.md): step-by-step setup.
- [k3d.yaml](../demo/k3d.yaml): local cluster definition.
- [eso-gcpsm-css.yaml](../demo/eso-gcpsm-css.yaml): ClusterSecretStore for GCPSM.
- [eso-gcpsm-es.yaml](../demo/eso-gcpsm-es.yaml): ExternalSecret resource.
- [demo-deploy.yaml](../demo/demo-deploy.yaml): example Deployment using synced secrets.

This demo shows how to bootstrap an environment using **GCP Secret Manager**, **External Secrets Operator**, **Reflector**, and **Reloader** within a local **k3d** cluster.

➡️ Next: [Problems](problems.md)
