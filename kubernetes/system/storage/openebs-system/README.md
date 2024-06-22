# openebs

Quick start installation [guide](https://openebs.io/docs/quickstart-guide/installation)

Install driver on node before installing `ZFS`. See [documentation](https://openebs.io/docs/user-guides/local-storage-user-guide/local-pv-zfs/zfs-installation)

```bash
helm install openebs . -n openebs-system --create-namespace
```
