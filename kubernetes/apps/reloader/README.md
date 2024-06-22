# reloader

## Installation 

```bash
helm repo add stakater https://stakater.github.io/stakater-charts
helm install reloader stakater/reloader -n reloader --create-namespace
```

## Configuration

More info [here](https://github.com/stakater/Reloader/blob/master/README.md).

Add the following annotation on deployment
```yaml
kind: Deployment
metadata:
  annotations:
    reloader.stakater.com/auto: "true"
spec:
  template:
    metadata:
```