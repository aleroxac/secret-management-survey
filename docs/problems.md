# Problems in Secret Management

Kubernetes offers native `Secret` objects, but they are **not truly encrypted**, only Base64-encoded.  
This creates several systemic weaknesses:

### 1. Plaintext Exposure
Anyone with access to `kubectl get secrets -o yaml` can read sensitive data.

### 2. GitOps Dilemma
Secrets cannot be versioned securely in Git without an additional encryption layer.

### 3. Rotation and Consistency
Without automation, rotating credentials (e.g., DB passwords) requires manual sync across clusters and manifests.

### 4. Duplication
When multiple apps share the same secret (e.g., a common DB), each namespace tends to have duplicated copies.

### 5. Lack of Audit and Lifecycle Control
Native secrets provide no audit trail, version history, or lifecycle management.

---

➡️ Continue to [Solutions](solutions.md)
