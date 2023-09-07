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