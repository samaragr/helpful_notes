## Pod

```YAML
apiVersion: #version of kubernetes api
kind: Pod
metadata:
  name:
  labels: # e.g. app:, type:- can add what you choose here
spec:
  containers:
    -name:
    image
```


## Replication controller / Replica set

``` YAML
apiVersion: apps/<version>
kind: ReplicationController / ReplicaSet
metadata:
  name:
  labels: # e.g. app:, type:- can add what you choose here
spec:
  template: # Pod info
    metadata:
      name:
      labels:
    spec:
      containers:
        - name:
          image:
replicas: <no.>
selector: #for replicaSet
  matchLabels:
    type: front-end #example
```


## Deployment
#checkthis
``` YAML
apiVersion: apps/<version>
kind: Deployment
metadata:
  name:
  labels: # e.g. app:, type:- can add what you choose here
spec:
  template:
    metadata:
      name:
      labels:
    spec:
      containers:
        - name:
          image:
replicas: <no.>
selector: 
  matchLabels:
    type: front-end #example
```


## Services

``` YAML
apiVersion: v1 #example
kind: Service
metadata:
  name:
  labels: # e.g. app:, type:- can add what you choose here
spec:
  type:
  ports:
    - port: <port>
      targetPort: <port>
  selector:
```
