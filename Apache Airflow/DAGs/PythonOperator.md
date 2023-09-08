### PythonOperator
```
downloading_rates = PythonOperator(
    task_id="downloading_rates",
    python_callable=download_rates
)
```

Details: https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/python/index.html#airflow.operators.python.PythonOperator