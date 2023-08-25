### Always test the new task before running the entire pipeline
> docker exec -it [container_id] /bin/bash
> airflow tasks test [DAG_name] [task_id] [execution_date] 