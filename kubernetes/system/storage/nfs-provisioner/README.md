# nfs-external-provisioner

The NFS subdir external [provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner) is an automatic provisioner for Kubernetes that uses your already configured NFS server, automatically creating Persistent Volumes.

## Installation 

More information in [readme](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner/blob/master/charts/nfs-subdir-external-provisioner/README.md).

```bash
# On client, install nfs-common
apt-get install nfs-common -y

helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/

helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner --set nfs.server=192.168.10.252 --set nfs.path=/volume1/nfs/kubernetes --set storageClass.reclaimPolicy=Retain -n nfs-provisioner --create-namespace

# OR

helm install nfs-subdir-external-provisioner . -n nfs-provisioner --create-namespace
```

After the installation, the storageClassName to use is `nfs-client`.

## Usage

Pod config
```yaml
kind: Pod
apiVersion: v1
metadata:
  name: test-pod
spec:
  containers:
  - name: test-pod
    image: busybox:stable
    command:
      - "/bin/sh"
    args:
      - "-c"
      - "touch /mnt/SUCCESS && exit 0 || exit 1"
    volumeMounts:
      - name: nfs-pvc
        mountPath: "/mnt"
  restartPolicy: "Never"
  volumes:
    - name: nfs-pvc
      persistentVolumeClaim:
        claimName: test-claim
```

PVC config
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: test-claim
spec:
  storageClassName: nfs-client
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Mi
```