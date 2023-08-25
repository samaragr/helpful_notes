## Test DAGs with Pytest in Staging environment
<mark>https://github.com/marclamberti/airflow-eks-docker</mark>

##### Run the unit-test:
> docker build -t airflow-test [project-folder]

the `project-folder` contains the directories:
- `unittests`
- `dags`

Verify Docker image `airflow-test` exists:
> docker image ls

Run specific unit-test file:
> docker run --rm airflow-test bash -c "airflow initdb && pytest unittests/test_dag_validation.py" 

##### Run unit-test at CodePipeline:
- Edit the `airflow-dev-pipeline.cfn.yaml` file, add following under `CodeBuildProject` section `build`:
```
build:
    commands:
    - echo Build started on `date`
    - docker build -t "${REPOSITORY_URI}:latest" .
    - docker tag "${REPOSITORY_URI}:latest" "${REPOSITORY_URI}:${TAG}"
    - docker run --rm "${REPOSITORY_URI}:latest" bash -c "airflow initdb && pytest unittest
post_build:
    ....
```

This will execute all the unit-tests in the project folder.

- Execute `aws cloudformation` command `update-stack`:
> aws cloudformation update-stack --stack-name=airflow-dev-pipeline --template-body=file://path/to/file/airflow-dev-pipeline.cfn.yml --parameters ParameterKey=GitHubUser,ParameterValue=[username] ParameterKey=GitHubToken,ParameterValue=[paste token value here] ParameterKey=GitSourceRepo,ParameterValue=airflow-eks-docker ParameterKey=GitBranch,ParameterValue=dev

- Updating the DAGs airflow docker project will trigger the pipeline and run unit-tests.

