## Intro
1. Container runtime for ECS and EKS
2. Serverless Kubernetes
3. Pay only for Pod execution time

## Create cluster
> `vim fargate-profile.yaml`
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: EKS-cluster-fargate
  region: us-west-2
fargateProfiles:
  - name: fargate-app
    selectors:
      - namespace: default
      - namespace: kube-system
  - name: staging
    selectors:
      - namespace: staging
        labels:
          env: staging
          checks: passed
```
> `eksctl create cluster -f fargate-profile.yaml`

- Verify in AWS CloudFormation
- Verify in AWS EKS clusters page
- Verify `kubectl` command
> kubectl get nodes
> kubectl get pods --all-namespaces

## Delete fargate cluster
> `eksctl delete cluster --name EKS-cluster-fargate`
