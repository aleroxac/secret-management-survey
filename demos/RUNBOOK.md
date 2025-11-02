# RUNBOOK — Secret Management E2E Demo

This runbook is part of the **Secret Management E2E Demo** documented in [README.md](README.md).  
It provides the detailed operational steps, validation, and troubleshooting instructions that complement the overview and architecture described in the README.

---

# Runbook

## K3D
``` shell
# Installation
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

# Create the cluster
k3d cluster create --config k3d.yaml

## Check if all pods are ready
kubectl get pods --all-namespaces
```



## GCP IAM
``` shell
echo -n "Enter the GCP project ID: " && read GCP_PROJECT_ID
echo -n "Enter the GCP custom role name: " && read GCP_ROLE_NAME
echo -n "Enter the GCP service account name: " && read GCP_SA_NAME
echo -n "Enter the path to store the GCP service account key file: " && read GCP_SA_KEY_FILE_PATH

# Creating the GCP custom role
gcloud iam roles create "${GCP_ROLE_NAME}" \
    --stage=GA \
    --permissions="secretmanager.versions.access" \
    --project=${GCP_PROJECT_ID}

# Creating the GCP service account
gcloud iam service-accounts create "${GCP_SA_NAME}" \
    --project=${GCP_PROJECT_ID}

# Linking the GCP custom role with the service account
gcloud projects add-iam-policy-binding ${GCP_PROJECT_ID} \
    --member="serviceAccount:${GCP_SA_NAME}@${GCP_PROJECT_ID}.iam.gserviceaccount.com" \
    --role="projects/${GCP_PROJECT_ID}/roles/${GCP_ROLE_NAME}" \
    --project="${GCP_PROJECT_ID}"

# Creating a GCP service account key
gcloud iam service-accounts keys create "${GCP_SA_KEY_FILE_PATH}" \
    --iam-account="${GCP_SA_NAME}@${GCP_PROJECT_ID}.iam.gserviceaccount.com" \
    --project="${GCP_PROJECT_ID}"
```



## GCP Secret Manager
``` shell
# Create some dummy secrets
for env in dev stg prd sdx; do
    gcloud secrets create demo-${env} \
        --project="${GCP_PROJECT_ID}" \
        --data-file=<(echo "{\"ENV\": \"${env}\"}")
done

# Creating a secret to store the GCP service accont key content
gcloud secrets create "${GCP_SA_NAME}-sa-key" \
    --data-file="${GCP_SA_KEY_FILE_PATH}" \
    --project="${GCP_PROJECT_ID}"
```



## External Secrets Operator
``` shell
helm repo update && helm repo add external-secrets https://charts.external-secrets.io
helm upgrade --install external-secrets external-secrets/external-secrets -n external-secrets --create-namespace
kubectl get pods -n external-secrets


kubectl create secret generic eso-provider-gcpsm-creds \
    --from-file=gcp-sa-key.json="${GCP_SA_KEY_FILE_PATH}" \
    -n external-secrets
sed "s/GCP_PROJECT_ID/${GCP_PROJECT_ID}/g" eso-gcpsm-css.yaml | kubectl apply -f-
kubectl wait --for=condition=ready css/gcpsm -n external-secrets
```



## K8S secret and deployment
``` shell
kubectl create ns demo
kubectl apply -f eso-gcpsm-es.yaml

kubectl wait --for=condition=ready es/demo-dev -n demo
kubectl get secret demo-dev -o go-template="{{ .data.ENV | base64decode }}"

kubectl apply -f demo-deploy.yaml
kubectl wait --for=condition=ready pods -l app=demo -n demo
```



## Playground-01: eso + (secret + deploy)
``` shell
# terminal-01
kubectl logs -f -l app=demo -n demo

# terminal-02
gcloud secrets versions add --secret=demo-dev --data-file=<(echo '{"ENV": "develop"}')
kubectl rollout restart deploy/demo -n demo
kubectl wait --for=condition=ready pods -l app=demo -n demo
```

## Playground-01: (eso + reloader) + (secret + deploy)
``` shell
helm repo add stakater https://stakater.github.io/stakater-charts
helm install reloader stakater/reloader -n kube-system

metadata:
  annotations:
    secret.reloader.stakater.com/reload: "demo-dev"
```



## References
- https://k3d.io/stable/usage/configfile/
- https://artifacthub.io/packages/helm/external-secrets-operator/external-secrets
- https://external-secrets.io/latest/introduction/getting-started/
