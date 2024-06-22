# home-ops 🏠🤖

My personal Kubernetes cluster orchestrated by [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) and [Renovate](https://docs.renovatebot.com/) 

## Bootstrap

1. kubernetes/system/network/cilium
```bash
helm install cilium kubernetes/system/network/cilium -n kube-system
```
2. kubernetes/system/network/coredns
```bash
# Attention, in the first install, disable monitoring unless the monitore is already installed
helm install coredns kubernetes/system/network/coredns -n kube-system
```

## Local certificate and domain management

```mermaid
graph TD
    subgraph HashiCorp Vault
        A[Root PKI]
        B[Intermediate PKI]
    end

    1[Ingress Created] -->|1| 2[Cert Manager]
    1 -->|1| 6[External DNS]
    6 -->|2| 7[Pi-hole DNS]
    2 -->|2| 3[Certificate Request]
    3 -->|3| B
    B -->|4| 4[Signed Certificate]
    4 -->|5| 2
    2 -->|6| 5[Certificate Ready]
```