#### Intro
Trigger rules determine when a task should be triggered based on the status of its upstream tasks.

```
@task(trigger_rule=TriggerRule.ONE_FAILED, retries=0)
def watcher():
    raise AirflowException("Failing task because one or more upstream tasks failed.")


with DAG(
    dag_id="watcher_example",
    schedule="@once",
    start_date=datetime(2021, 1, 1),
    catchup=False,
) as dag:
    failing_task = BashOperator(task_id="failing_task", bash_command="exit 1", retries=0)
    passing_task = BashOperator(task_id="passing_task", bash_command="echo passing_task")
    teardown = BashOperator(
        task_id="teardown",
        bash_command="echo teardown",
        trigger_rule=TriggerRule.ALL_DONE,
    )

    failing_task >> passing_task >> teardown
    list(dag.tasks) >> watcher()
```