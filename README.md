# 🔐 Secret Management Research

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Secret%20Management-326ce5)
![Status](https://img.shields.io/badge/Status-Research%20Complete-green)

---

## 📘 Overview

This repository contains my personal research on **secure secret management** for Kubernetes environments.

The study explores:
- How different tools handle secrets (ESO, CSI, SOPS, Sealed Secrets).
- Problems with Kubernetes native secrets.
- Approaches to achieving a **complete end-to-end Secret Encryption Lifecycle**.

👉 Full documentation: [📖 docs/overview.md](docs/overview.md)

---

## 🧪 Demo Environment

A working demo is available under [`/demos`](demos):

| File | Description |
|------|--------------|
| [k3d.yaml](demos/k3d.yaml) | Local cluster definition |
| [eso-gcpsm-css.yaml](demos/eso-gcpsm-css.yaml) | ClusterSecretStore (GCP Secret Manager) |
| [eso-gcpsm-es.yaml](demos/eso-gcpsm-es.yaml) | ExternalSecret example |
| [demo-deploy.yaml](demos/demo-deploy.yaml) | Example Deployment |
| [RUNBOOK.md](demos/RUNBOOK.md) | Step-by-step setup guide |

The demo showcases how to integrate **GCP Secret Manager**, **External Secrets Operator**, **Reflector**, and **Reloader** within a **k3d cluster**, providing a foundation for exploring the full lifecycle of secret synchronization and rollout.
