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
