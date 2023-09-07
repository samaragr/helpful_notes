- use BashOperator to save file in HDFS
```
saving_rates = BashOperator(
    task_id="saving_rates",
    bash_command="""
        hdfs dfs -mkdir -p /forex && \
        hdfs dfs -put -f $AIRFLOW_HOME/dags/files/forex_rates.json /forex
    """
)
```

### Basic usage
```
run_this = BashOperator(
    task_id="run_after_loop",
    bash_command="echo 1",
)
```

### Jinja Templating
```
also_run_this = BashOperator(
    task_id="also_run_this",
    bash_command='echo "ti_key={{ task_instance_key_str }}"',
)
```

```
bash_task = BashOperator(
    task_id="bash_task",
    bash_command="echo \"here is the message: '$message'\"",
    env={"message": '{{ dag_run.conf["message"] if dag_run else "" }}'},
)
```

### Skipping
```
this_will_skip = BashOperator(
    task_id="this_will_skip",
    bash_command='echo "hello world"; exit 99;',
    dag=dag,
)
```

### Troubleshooting
##### Jinja template not found
Add `space` in the end of bash_command argument
```
t2 = BashOperator(
    task_id="bash_example",
    # This fails with 'Jinja template not found' error
    # bash_command="/home/batcher/test.sh",
    # This works (has a space after)
    bash_command="/home/batcher/test.sh ",
    dag=dag,
)
```