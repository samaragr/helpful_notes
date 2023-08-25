### DAG start_date wth schedule_interval
```
from datetime import datetime, timedelta

default_args = {
    'start_date': datetime(2019, 3, 29, 1),
    'owner': 'Airflow'
}

with DAG(dag_id='start_and_schedule_dag', schedule_interval="0 * * * *", default_args=default_args) as dag:
    ...
```

Crontab generator:
https://crontab.guru

Alternatively, use `timedelta()` object:
```
schedule_internal=timedelta(hours=1)
```

### Backfill and catchup
Kick off the missing DAG runs

```
with DAG(... catchup=True/False) as dag:
```

or 
> vim airflow.cfg
```
catchup_by_default = True/False
```

or, run backfill manually
> airflow backfill -s 2019-01-20 -e 2019-01-25 --rerun_failed_tasks -B backfill

### Timezone
- use datetime.datetime()
- import airflow.timezone
- default to UTC

### Tasks dependent
- depends_on_past = True/False
- wait_for_downstream = True/False

### DAG folder structure
- parameter `dags_folder`
- absolute path by default: `$AIRFLOW_HOME/dags`
- ZIP
> zip -rm package_dag.zip packaged_dag.py functions/

Place the zip file on root of `dags` folder, Airflow can load it automatically.

- DagBag
```
# Script to add new DAGs folders using 
# the class DagBag
# Paths must be absolute
import os
from airflow.models import DagBag
dags_dirs = [
                '/usr/local/airflow/project_a', 
                '/usr/local/airflow/project_b'
            ]

for dir in dags_dirs:
   dag_bag = DagBag(os.path.expanduser(dir))

   if dag_bag:
      for dag_id, dag in dag_bag.dags.items():
         globals()[dag_id] = dag
```

`project-a` and `project-b` are sub-folders accessible by Airflow. It will automatically separate the DAGs according to the DagBags for different projects/teams. 

If server is not restarted after making changes to DAGs code, no errors will show on Airflow UI, but available on webserver log `docker logs -f [container_id]`

- `.airflowignore` file

### Web server config
- `web_server_master_timeout` default to 2 minutes
- workers default to `4 sync`, workers are refreshed when the webserver times out.
- `logging_level`, never set to `INFO` in production.

### Dag failure detections
DAG level:
- dagrun_timeout
- sla_miss_callback
- on_failure_callback
- on_success_callback

Task level:
- email
- email_on_failure
- email_on_retry
- retries
- retry_delay
- retry_exponential_backoff
- max_retry_delay
- execution_timeout
- on_failure_callback
- on_success_callback
- on_retry_callback

Example:
```
from airflow import DAG
from airflow.operators.bash_operator import BashOperator

from datetime import datetime, timedelta

default_args = {
    'start_date': datetime(2019, 1, 1),
    'owner': 'Airflow'
}

with DAG(dag_id='alert_dag', schedule_interval="0 0 * * *", default_args=default_args, catchup=True) as dag:
    
    # Task 1
    t1 = BashOperator(task_id='t1', bash_command="exit 1")
    
    # Task 2
    t2 = BashOperator(task_id='t2', bash_command="echo 'second task'")

    t1 >> t2
```