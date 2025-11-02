# CSI Secret Store Driver

The **Secrets Store CSI Driver** allows Kubernetes workloads to **mount secrets directly from external providers**, without storing them as `Secret` objects in etcd.

---

## 🧱 Architecture

```
External Secret Store → CSI Driver → Pod Volume (mounted secret)
```

This approach avoids storing plaintext secrets in the cluster altogether.

---

## ⚙️ Example Configuration

```yaml
volumes:
- name: secrets-store-inline
  csi:
    driver: secrets-store.csi.k8s.io
    readOnly: true
    volumeAttributes:
      secretProviderClass: gcpsm-provider
```

---

## ✅ Advantages

| Feature | Description |
|----------|-------------|
| 🔒 No plaintext in etcd | Secrets are fetched on demand. |
| ⚙️ Native Rotation | Secrets update without reapplying manifests. |
| 🧩 Integration | Compatible with GCP, AWS, Vault, etc. |

---

## ❌ Trade-offs

| Limitation | Description |
|-------------|-------------|
| ⚙️ Complex Setup | Requires CSI driver and provider config. |
| 🚫 Limited EnvVar Mapping | Secrets are mounted as files, not env vars. |
| 🧱 Custom Integration | Apps must read secrets from files. |

---

**Next:** [Zero Trust Secret Flow →](zero-trust-flow.md)
