# DIPS Smart on FHIR Sandbox

## Description

This chart deploys the DIPS Smart on FHIR Sand Box. This is the very beginning of a sand box for running Smart On FHIR apps in a simulated EHR. The running system consists of a frontend written in React and three backend services written in node/express.

### dips-ehr-app

This is the front end. It calls the given fhir-service and loads all patients in list at the left. In the dropbox you can choose between configured Smart on FHIR App. Select a patient in the list to load the Smart on FHIR app with this patient in context.

The about tab shows the current configuration for the app.

### dips-ehr-configuration

The is a simple wrapper over a json hosted at github. All changes to the configuration is done by editing the json file at github. Be aware that due to caching the <https://raw.githubusercontent.com/> - site some times is not updated before after five minutes.
See [repo](../dips-ehr-configuration) for the code and more documentation.

### dips-ehr-security

Service implementing the client credentials flow for Smart on FHIR apps hosted in en EHR.
See [repo](../dips-ehr-security) for the code and more documentation.

The Client Credentials Flow
![The Client Crendentials Flow](./images/clientcredentialsflow-white.png)

### dips-fhir-service

Simple service implementing the FHIR-calls needed for our sand box. The services serves content stored as flat json files generated by [Synthea](https://synthea.mitre.org/).

## Requirements:
- Docker & Kubernetes: https://docs.docker.com/install/
- python: https://www.python.org/downloads/
- Helm 3+: https://helm.sh/docs/intro/install/
- Azure cli: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest

Add [ingress-nginx](https://kubernetes.github.io/ingress-nginx/) to helm repo:
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/
```


## Installation

### Commands

### Create Sandbox environment
```
kubectl create namespace ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx

cd helm\SandBox
kubectl create namespace sandbox
helm install sandbox . --namespace sandbox
```

### Useful commands

See everything:
kubectl get pods --all-namespaces -o wide

#### Fix hanging ingress resources

kubectl get ValidatingWebhookConfiguration --all-namespaces
kubectl get ClusterRoleBinding --all-namespaces

kubectl delete ClusterRoleBinding [name]
