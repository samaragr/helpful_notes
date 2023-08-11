Type: #AWS #EKS #kubernetes #eksctl 

## Commands
- `eksctl create cluster` - create cluster using default params
	- default:
		- two m5.large worker nodes
		- uses official EKS AMI
		- us-west-2 region
		- dedicated VPC
	- `-f <cluster>.yml` - customise using YAML file
		- 
