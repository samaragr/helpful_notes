Type: #kubernetes #cheatsheet 

## Kubectl commands
- `kubectl get`
	- `pods`-  get all pods
	- `nodes` - get all nodes
		- `-o wide` - get nodes with extra info
	- `replicaset` - see list of replicas
		- `rs` - also works
	- `all` 
	- `deployments`
- `kubectl create` -
	- `-f <file-name.yml>` - create a resource from manifest file
- `kubectl apply` - 
	- `-f <file-name.yml` - apply manifest file
- `kubectl edit pod <pod-name>`
- `kubectl run <pod>` 
	- `--image=<image>` - create a new Pod from image
	- `--dry-run=client -o yaml > <file-name.yml.>` - create a manifest file
- `kubectl describe <pod> <podId>` - describe pod info
- `kubectl delete` 
	- `pod <podname>` - delete pod
	- `replicaset <name>` - also deletes all underlying Pods
- `kubectl replace` - replace or update replicaset
- `kubectl scale` - scale from command line without having to replace file
	- `--replicas=<no.> -f <file-name.yml>`
- `kubectl rollout` 
	- `status <deployent-name>` 
	- `history <deployent-name>` 
	- `undo <deployent-name>`
