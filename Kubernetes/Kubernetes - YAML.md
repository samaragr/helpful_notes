## Pod
- `apiVersion:` - version of kubernetes api
- `kind: Pod`
- `metadata:`
	- `name:`
	- `labels:`
		- e.g. `app:`, `type:`- can add what you choose here
- `spec:`
	- `containers:`
		- `-name:`
		- `image:`

## Replication controller / Replica set
- `apiVersion: apps/<version>` - version of kubernetes api
- `kind: ReplicationController / ReplicaSet` 
- `metadata:`
	- `name:`
	- `labels:`
		- e.g. `app:`, `type:`- can add what you choose here
- `spec:`
	- `template:` - from Pod info
		- `metadata:`
			- `name:`
			- `labels:`
		- `spec:`
			- `containers:`
				- `-name:`
				- `image:`
	- `replicas: <no.>`
	- `selector:` ==*replica set*==
		- `matchLabels:`
			- `type: front-end`  

## Deployment
- `apiVersion: apps/v1`
- `kind: Deployment`
- `metadata:`
	- `name:`
	- `labels:`
		- e.g. `app:`, `type:`- can add what you choose here
- `spec:`
	- `template:` - from Pod info
		- `metadata:`
			- `name:`
			- `labels:`
		- `spec:`
			- `containers:`
				- `-name:`
				- `image:`
	- `replicas: <no.>`
	- `selector:` ==*replica set*==
		- `matchLabels:`
			- `type: front-end`  



## Services
- `apiVersion: v1` - version of kubernetes api
- `kind: Service` 
- `metadata:`
	- `name:`
	- `labels:`
		- e.g. `app:`, `type:`- can add what you choose here
- `spec:`
	- `type:`
	- `ports:`
		- `- port: <port>`
		-     `targetPort: <port>`
	- `selector:`
	- 