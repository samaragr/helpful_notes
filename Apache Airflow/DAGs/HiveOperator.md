### Add new connection
conn_id: `hive_conn`
conn_type: `HIVE Server 2 Thrift`
host: `hive-server`
login: `hive`
password: `hive`
port: `10000`

### DAG task
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

### SQL like queries
Logon to Hue, select the database, then query:
```
SELECT * FROM `default`.`forex_rates` LIMIT 100;
```

https://airflow.apache.org/docs/apache-airflow-providers-apache-hive/stable/_api/airflow/providers/apache/hive/operators/hive/index.html

