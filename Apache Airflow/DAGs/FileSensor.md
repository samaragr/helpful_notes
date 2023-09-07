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
Create new connection in Airflow Amin
conn_id: `forex_path`
conn_type: `File(path)`
host: <empty>
extra: `{"path":"/opt/airflow/dags/files"}`