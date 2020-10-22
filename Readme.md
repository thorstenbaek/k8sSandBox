# DIPS Smart n FHIR Sandbox Chart

## Prerequiries:
- Kubernetes 
- Cluster
- Helm

## Commands

### Create Sandbox environment

kubectl create namespace sandbox

helm install sandbox ingress-nginx/ingress-nginx --namespace sandbox

cd helm\SandBox
helm install