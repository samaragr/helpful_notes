- Create connection
conn id: forex_api
conn type: HTTP
host: https://gist.github.com/

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

Details: 
https://airflow.apache.org/docs/apache-airflow-providers-http/stable/_api/airflow/providers/http/sensors/http/index.html#module-airflow.providers.http.sensors.http