### Python package - Airflow Sensors
https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/sensors/index.html

- FileSensor
```
is_forex_currencies_file_available = FileSensor(
    task_id="is_forex_currencies_file_available",
    fs_conn_id="forex_path",
    filepath="forex_currencies.csv",
    poke_interval=5,
    timeout=20
)
```

- HttpSensor
```
is_forex_rates_available = HttpSensor(
    task_id="is_forex_rates_available",
    http_conn_id="forex_api",
    endpoint="marclamberti/f45f872dea4dfd3eaa015a4a1af4b39b",
    response_check=lambda response: "rates" in response.text,
    poke_interval=5,
    timeout=20
)
```

### PythonOperator
```
downloading_rates = PythonOperator(
    task_id="downloading_rates",
    python_callable=download_rates
)
```

Details: https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/python/index.html#airflow.operators.python.PythonOperator

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

### HiveTable
1. Add new connection in Airflow


2. Add python code in DAGs
```
creating_forex_rates_table = HiveOperator(
    task_id="creating_forex_rates_table",
    hive_cli_conn_id="hive_conn",
    hql="""
        CREATE EXTERNAL TABLE IF NOT EXISTS forex_rates(
            base STRING,
            last_update DATE,
            eur DOUBLE,
            usd DOUBLE,
            nzd DOUBLE,
            gbp DOUBLE,
            jpy DOUBLE,
            cad DOUBLE
            )
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY ','
        STORED AS TEXTFILE
    """
)
```

HIVE Operator doc: https://airflow.apache.org/docs/apache-airflow-providers-apache-hive/stable/_api/airflow/providers/apache/hive/operators/hive/index.html

### Spark submit operator to submit a Spark job
1. Airflow Admin -> Add Connection
Conn Id: spark_conn
Conn type: Spark
host: spark://spark-master
port: 7077

2. Python code in DAGs
```
forex_processing = SparkSubmitOperator(
    task_id="forex_processing",
    application="/opt/airflow/dags/scripts/forex_processing.py",
    conn_id="spark_conn",
    verbose=False
)
```

Details: 
https://airflow.apache.org/docs/apache-airflow-providers-apache-spark/stable/index.html
https://airflow.apache.org/docs/apache-airflow-providers-apache-spark/stable/_api/airflow/providers/apache/spark/hooks/spark_submit/index.html


Spark application `forex_processing.py`:
```
from os.path import expanduser, join, abspath

from pyspark.sql import SparkSession
from pyspark.sql.functions import from_json

warehouse_location = abspath('spark-warehouse')

# Initialize Spark Session
spark = SparkSession \
    .builder \
    .appName("Forex processing") \
    .config("spark.sql.warehouse.dir", warehouse_location) \
    .enableHiveSupport() \
    .getOrCreate()

# Read the file forex_rates.json from the HDFS
df = spark.read.json('hdfs://namenode:9000/forex/forex_rates.json')

# Drop the duplicated rows based on the base and last_update columns
forex_rates = df.select('base', 'last_update', 'rates.eur', 'rates.usd', 'rates.cad', 'rates.gbp', 'rates.jpy', 'rates.nzd') \
    .dropDuplicates(['base', 'last_update']) \
    .fillna(0, subset=['EUR', 'USD', 'JPY', 'CAD', 'GBP', 'NZD'])

# Export the dataframe into the Hive table forex_rates
forex_rates.write.mode("append").insertInto("forex_rates")
```

3. test the task: 
> airflow tasks test forex_data_pipeline forex_processing 2021-01-01

### EmailOperator
1. configure email provider
Login to https://security.google.com/settings/security/apppasswords
Select Mail as App for Mac, generate the password and copy it.

2. Configure airflow 
> vim airflow/airflow.cfg

Configure [smtp] section

3. Restart Docker
4. Add `emailOperator` to DAGs
```
from airflow.operators.email import EmailOperator

send_email_notification = EmailOperator(
    task_id="send_email_notification",
    to="airflow_course@yopmail.com",
    subject="forex_data_pipeline",
    html_content="<h3>forex_data_pipeline</h3>"
)
```

### Slack notification with the Slack Webhook operator
1. Slack.com
2. Create a new workspace
3. Create an application: api.slack.com/apps, add Incoming Webhooks to the workspace. Copy the Webhook URL
4. Configure DAGs code
```
from airflow.providers.slack.operators.slack_webhook import SlackWebhookOperator

def _get_message() -> str:
    return "Hi from forex_data_pipeline"

with DAG("forex_data_pipeline", start_date=datetime(2021, 1 ,1), 
    schedule_interval="@daily", default_args=default_args, catchup=False) as dag:
    ...    
    send_slack_notification = SlackWebhookOperator(
        task_id="send_slack_notification",
        http_conn_id="slack_conn",
        message=_get_message(),
        channel="#monitoring"
    )
``` 
5. Create Airflow Connection
Conn id: slack_conn
Conn type: HTTP
Password: `[paste the webhook URL]`

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
