# Introduction

This documentation compiles my research on **Secret Management in Kubernetes**, exploring existing tools, patterns, and the security gaps they attempt to solve.  

As I evolved my understanding, I moved from simple `Kubernetes Secrets` to more advanced and centralized solutions, seeking an **end-to-end Secret Encryption Lifecycle** — from storage to application runtime.

The goal is to:
- Understand the **limitations** of native Kubernetes secret storage.
- Compare **GitOps-oriented encryption** (e.g., SOPS, Sealed Secrets) vs **Runtime Sync solutions** (ESO, CSI Drivers).
- Design a **secure, automated, and reproducible** model to manage secrets across environments.

➡️ Continue to [Overview](overview.md)
