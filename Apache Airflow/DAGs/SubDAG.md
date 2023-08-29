### Minimise repetitive patterns with SubDAGs
1. Create a Factory Function -> creates 5 DAG Object
```
from airflow.models import DAG
from airflow.operators.dummy_operator import DummyOperator

def factory_subdag(parent_dag_name, child_dag_name, default_args):

    with DAG(
        dag_id='%s.%s' % (parent_dag_name, child_dag_name),
        default_args=default_args
    ) as dag:

        for i in range(5):
            DummyOperator(
                task_id='%s-task-%s' % (child_dag_name, i + 1)
            )

    return dag
```
2. SubDagOperator
```
from subdags.subdag import factory_subdag
from airflow.operators.subdag_operator import SubDagOperator

subdag_1 = SubDagOperator(
        task_id='subdag-1',
        subdag=factory_subdag(DAG_NAME, 'subdag-1', default_args),
        executor=SequentialExecutor()
    )

subdag_2 = SubDagOperator(
        task_id='subdag-2',
        subdag=factory_subdag(DAG_NAME, 'subdag-2', default_args),
        executor=SequentialExecutor()
    )

```

or execute tasks in parallel in Production:
```
from subdags.subdag import factory_subdag
from airflow.operators.subdag_operator import SubDagOperator

subdag_1 = SubDagOperator(
        task_id='subdag-1',
        subdag=factory_subdag(DAG_NAME, 'subdag-1', default_args),
        executor=CeleryExecutor()
    )

subdag_2 = SubDagOperator(
        task_id='subdag-2',
        subdag=factory_subdag(DAG_NAME, 'subdag-2', default_args),
        executor=CeleryExecutor()
    )

```