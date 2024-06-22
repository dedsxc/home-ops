# external-secret

## Installation

```bash
helm repo add external-secrets https://charts.external-secrets.io

helm install external-secrets \
   external-secrets/external-secrets \
    -n external-secrets \
    --create-namespace
```

More information: [here](https://external-secrets.io/latest/introduction/getting-started/)