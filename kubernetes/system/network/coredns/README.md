# Core-dns


## Installation

Setup cluster dns ip with k3s
```bash
k3s server ... --cluster-dns 10.43.0.10
```

```bash
helm repo add coredns https://coredns.github.io/helm
helm --namespace=kube-system install coredns coredns/coredns --set service.clusterIP=10.43.0.10

# or
helm install coredns . -n kube-system
```