# Ingress-nginx

More info [nginx](https://kubernetes.github.io/ingress-nginx/deploy/)

## Installation

```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```