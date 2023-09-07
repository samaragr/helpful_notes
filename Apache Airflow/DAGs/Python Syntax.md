### Python package - Airflow Sensors
https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/sensors/index.html


### Add dependencies for the tasks
1. Set downstreams 
```
[task_id_A].set_downstream([task_id_B])
```

2. Set upstreams
```
[task_id_B].set_upstream([task_id_A])
```

3. Alternatively, use `>>` and `<<` instead
[task_id_A] >> [task_id_B] >> [task_id_C] >> [task_id_D]


### Template
Jinja templating engine
```
templated_command = dedent(
    """
{% for i in range(5) %}
    echo "{{ ds }}"
    echo "{{ macros.ds_add(ds, 7)}}"
{% endfor %}
"""
)

t3 = BashOperator(
    task_id="templated",
    depends_on_past=False,
    bash_command=templated_command,
)
```