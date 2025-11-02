# Demo — Secret Management E2E Example

This demo showcases a full implementation of the **GCP Secret Manager + External Secrets Operator + Reflector + Reloader** stack using a local **k3d cluster**.

---

## 🧭 Overview

This demo aims to simulate a **secure, automated, and centralized secret lifecycle** in Kubernetes.  
It integrates multiple layers of automation — from secret storage in GCP Secret Manager to rollout automation via Reloader.

---

## 🧰 Components

| Tool | Role |
|------|------|
| **k3d** | Lightweight local Kubernetes cluster |
| **GCP Secret Manager** | Centralized secret storage |
| **External Secrets Operator (ESO)** | Sync secrets from GCP to K8s |
| **Reflector** | Propagate secrets across namespaces |
| **Reloader** | Trigger app rollouts on secret changes |

---

## ⚙️ Quick Start

```bash
# 1. Create the cluster
k3d cluster create demo --config k3d.yaml

# 2. Install ESO, Reflector, and Reloader via Helm or manifests
kubectl apply -f eso-gcpsm-css.yaml
kubectl apply -f eso-gcpsm-es.yaml

# 3. Deploy the demo application
kubectl apply -f demo-deploy.yaml

# 4. Verify synchronization
kubectl get externalsecrets -A
kubectl get secrets -A
```

---

## 🔄 Secret Update Flow

When a secret is updated in **GCP Secret Manager**:

1. ESO detects the new version and syncs it.
2. Reflector replicates the update to all namespaces.
3. Reloader triggers application rollout automatically.
4. The app receives new environment variables seamlessly.

---

## 📘 Detailed Execution Guide

For a complete **step-by-step operational guide**, including troubleshooting and validation, see the [RUNBOOK.md](RUNBOOK.md).  
This readme provides context and overview — the **RUNBOOK** handles execution details.

---

## ✅ Validation Commands

```bash
kubectl describe externalsecret demo-dev -n demo
kubectl logs deploy/demo-app -n demo
```

---

## 🧩 Related Documentation

- [docs/encryption-lifecycle.md](../docs/encryption-lifecycle.md)
- [docs/zero-trust-flow.md](../docs/zero-trust-flow.md)
- [docs/secret-rotation.md](../docs/secret-rotation.md)
- [docs/rbac-iam.md](../docs/rbac-iam.md)
- [docs/compliance.md](../docs/compliance.md)

---

## 🧹 Cleanup

```bash
kubectl delete -f demo-deploy.yaml
k3d cluster delete demo
```

---

**Next:** Continue with the operational guide in [RUNBOOK.md](RUNBOOK.md).
