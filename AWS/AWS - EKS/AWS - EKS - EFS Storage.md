## Create namespace
> kubectl create namespace [namespace-name]

## Create AWS RowBinding
> vim create-rbac.yaml
```
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: nfs-provisioner-role-binding
subjects:
  - kind: ServiceAccount
    name: default
    namespace: [namespace-name]
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```
> kubectl apply -f create-rbac.yaml -n [namespace-name]

# Attach EFS for multi-zone pods
## Install aws-efs-csi-driver
> helm repo add aws-efs-csi-driver https://kubernetes.sigs.github.io/aws-efs-csi-driver
> helm install aws-efs-csi-driver aws-efs-csi-driver/aws-efs-csi-driver

## Create StorageClass
```
kind: StorageClass
apiVersoin: storage.k8s.io/v1
metadata:
  name: efs-sc
provisioner: efs.csi.aws.com
```

## Create persistent Volume
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: efs-pv-eks
spec:
  capacity:
    storage: 20Gi
  volumeMode: Filesystem
  accessModes: 
    - ReadWriteMany
  persistentVolumeRelaimPolicy: Retain
  storageClassName: efs-sc
  csi:
    driver: efs.csi.aws.com
    volumeHandle: fs-[efs-fs-id]
```

## Create persistent volume Claim
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: efs-claim
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: efs-sc
  resources:
    requests:
      storage: 20Gi
```

## To use the persistent volume claim
```
apiVersion: v1
metadata:
  name: ...
spec:
  containers:
  - image: ...
    name: ..
    volumeMounts:
    - name: persistent-storage-name
      mountPath: /local/path/in/container
  volumes:
  - name: persistent-storage-name
    persistentVolumeClaim:
      claimName: efs-claim
```

## Check persistent volume
> kubectl get pv --namespace=...

## Check persistent volume claim
> kubectl get pvc --namespace=...

## Check persisitent volume within EC2
1. get EC2 instance public DNS
2. login to EC2 instance: `> ssh -i server.pem ec2-user@ec2-xx-xx-xxx-xxx.us-west-2.compute.amazonaws.com`
3. Command: `> sudo mount | grep csi`

