# node feature discovery

This software enables node feature discovery for Kubernetes. It detects hardware features available on each node in a Kubernetes cluster, and advertises those features using node labels and optionally node extended resources, annotations and node taints. Node Feature Discovery is compatible with any recent version of Kubernetes (v1.21+).

More info: [here](https://kubernetes-sigs.github.io/node-feature-discovery/v0.15/get-started/introduction.html)

## Installation

```bash
# Kustomize
kubectl apply -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/default?ref=v0.15.4

# Helm
helm repo add nfd https://kubernetes-sigs.github.io/node-feature-discovery/charts
helm repo update
helm install nfd/node-feature-discovery --namespace node-feature-discovery --create-namespace --generate-name
```

## Configuration

Writing rule are describe [here](https://kubernetes-sigs.github.io/node-feature-discovery/v0.15/usage/customization-guide.html#custom-feature-source)

## Uninstallation

```bash
kubectl apply -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/prune?ref=v0.15.4
kubectl -n node-feature-discovery wait job.batch/nfd-master --for=condition=complete && kubectl delete -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/prune?ref=v0.15.4
```