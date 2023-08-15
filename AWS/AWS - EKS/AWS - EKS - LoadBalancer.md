## Create LoadBalander service
```
apiVersion: v1
kind: Service
metadata:
  name: app-name
  label:
    app: app-name
spec:
  ports:
    - port: 80
  selector:
    app: app-name
    tier: frontend
  type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-name
  labels:
    app: app-name
spec:
  selector:
    matchLabels:
      app: app-name
      tier: frontend
  strategry:
    type: Recreate
  template:
    metadata: 
      labels:
        app: app-name
        tier: frontend
    spec:
      containers:
      - image: ...
        name: app-name
        env:
          ...
        ports:
        - containerPort: 80
          name: app-name
        volumeMounts:
        - name: persistent-storage-name
          mountPath: /local/mounting/path
      volumes:
      - name: persistent-storage-name
        persistentVolumeClaim:
          claimName: efs-claim
```

