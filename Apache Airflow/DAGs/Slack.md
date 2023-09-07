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