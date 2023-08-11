Type: #AWS #EMR #EKS #kubernetes
## Knowledge points
- Kubernetes namespace
- Virtual cluster
- Submit Spark Job
- AWS CLI
- `eksctl` CLI
- Amazon EMR containers CLI
- Job template
  - Create and use
  - Paramaters
  - Access permission
- Pod template

## Important
- EKS cluster requires minimum `x5.xlarge` instance type
- To enable Logging, IAM policy requires permission to access the target destination (S3 location, CloudWatch log stream, log group, etc)

## Get started
#### Register EKS Cluster with EMR using AWS CLI
```
aws emr-containers create-virtual-cluster \
        --name <virtual_cluster_name> \
        --container-provider '{
            "id": "<cluster_name>",
            "type": "EKS",
            "info": {
                "eksInfo": {
                    "namespace": "<namespace_name>"
                }
            }
        }'
``` 

When EKS cluster is registered, EMR workloads are deployed to Kubernetes nodes and pods. 

#### Run Spark Job
##### StartJobRun
```
aws emr-containers start-job-run \
    --name <job_name> \
    --virtual-cluster-id <cluster_id> \
    --execution-role-arn <IAM_role_arn> \
    --virtual-cluster-id <cluster_id> \
    --release-label <<emr_release_label> \
    --job-driver '{
        "sparkSubmitJobDriver": {
            "entryPoint": <entry_point_location>,
            "entryPointArguments": ["<arguments_list>"],
            "sparkSubmitParameters": <spark_parameters>
        }
    }'
```

Example - Run Spark Python application:
https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/getting-started.html

Example - Submit a Job run with JSON file:
> aws emr-containers start-job-run --cli-input-json file://./start-job-run-request.json

```start-job-run-request.json
{
  "name": "myjob", 
  "virtualClusterId": "123456",  
  "executionRoleArn": "iam_role_name_for_job_execution", 
  "releaseLabel": "emr-6.2.0-latest", 
  "jobDriver": {
    "sparkSubmitJobDriver": {
      "entryPoint": "entryPoint_location",
      "entryPointArguments": ["argument1", "argument2", ...],  
       "sparkSubmitParameters": "--class <main_class> --conf spark.executor.instances=2 --conf spark.executor.memory=2G --conf spark.executor.cores=2 --conf spark.driver.cores=1"
    }
  }, 
  "configurationOverrides": {
    "applicationConfiguration": [
      {
        "classification": "spark-defaults", 
        "properties": {
          "spark.driver.memory":"2G"
         }
      }
    ], 
    "monitoringConfiguration": {
      "persistentAppUI": "ENABLED", 
      "cloudWatchMonitoringConfiguration": {
        "logGroupName": "my_log_group", 
        "logStreamNamePrefix": "log_stream_prefix"
      }, 
      "s3MonitoringConfiguration": {
        "logUri": "s3://my_s3_log_location"
      }
    }
  }
}
```

##### Spark-submit
1. Setup environment variables
```
export SPARK_HOME=spark-home
export MASTER_URL=k8s://Amazon EKS-cluster-endpoint
```

2. Submit Spark application
```
SPARK_HOME/bin/spark-submit \
    --class org.apache.spark.examples.SparkPi \
    --master $MASTER_URL \
    --conf spark.kubernetes.container.image=895885662937.dkr.ecr.us-west-2.amazonaws.com/spark/emr-6.10.0:latest \
    --conf spark.kubernetes.authenticate.driver.serviceAccountName=spark \
    --deploy-mode cluster \
    --conf spark.kubernetes.namespace=spark-operator \
    local:///usr/lib/spark/examples/jars/spark-examples.jar 20
```

## Amazon EMR Studio
- No addtiional cost
- Jupyter notebook
- Real-time collaboration
- Debugging using Spark UI
- SQL Explorer
- Use GIT repository to trigger pipeline
- Chain notebooks to build pipelines
- Integrate notebooks into Amazon Airflow
- Re-attach notebooks to bigger cluster to run a job
  

## Run jobs for the Nvidia RAPIDS Accelerator for Apache Spark
1. Add GPU enabled node group
```
aws eks create-nodegroup \
    --cluster-name EKS_CLUSTER_NAME \
    --nodegroup-name NODEGROUP_NAME \
    --scaling-config minSize=0,maxSize=5,desiredSize=2 CHOOSE_APPROPRIATELY \
    --ami-type AL2_x86_64_GPU \
    --node-role NODE_ROLE \
    --subnets SUBNETS_SPACE_DELIMITED  \
    --remote-access ec2SshKey= SSH_KEY \
    --instance-types GPU_INSTANCE_TYPE \
    --disk-size DISK_SIZE \
    --region AWS_REGION
 ```

2. Install Nvidia device plugin
> kubectl apply -f https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/v0.9.0/nvidia-device-plugin.yml

3. Validate GPUs on each node in the cluster
> kubectl get nodes  "-o=custom-columns=NAME:.metadata.name,GPU:.status.allocatable.nvidia\.com/gpu"

4. Run Spark RAPIDS job
```
aws emr-containers start-job-run \
    --virtual-cluster-id VIRTUAL_CLUSTER_ID \
    --execution-role-arn JOB_EXECUTION_ROLE \
    --release-label emr-6.9.0-spark-rapids-latest \
    --job-driver '{"sparkSubmitJobDriver": {"entryPoint": "local:///usr/lib/spark/examples/jars/spark-examples.jar","entryPointArguments":  ["10000"], "sparkSubmitParameters":"--class org.apache.spark.examples.SparkPi "}}' \
    ---configuration-overrides '{"applicationConfiguration": [{"classification": "spark-defaults","properties": {"spark.executor.instances": "2","spark.executor.memory": "2G"}}],"monitoringConfiguration": {"cloudWatchMonitoringConfiguration": {"logGroupName": "LOG_GROUP _NAME"},"s3MonitoringConfiguration": {"logUri": "LOG_GROUP_STREAM"}}}'