# zabbix-alert-slack
Alertscript posting to slack.com

![Slack](https://raw.githubusercontent.com/uyorum/zabbix-alert-slack/master/img/image001.png)

## Usage
### 1. Get incoming webhook url
1. (If not) Create a channel in [slack.com](https://slack.com/)
1. Get an incoming webhook url [here](https://my.slack.com/services/new/incoming-webhook/).

### 2. Get this script
1. Put this script in Zabbix alertscript directory.
1. Add an execution permission

    ```bash
    # cd /usr/local/share/zabbix/alertscripts/
    # wget https://raw.githubusercontent.com/uyorum/zabbix-alert-slack/master/slack
    # chmod +x slack
    ```

### 3. Register as media
1. Administration -> Media types -> Create media type, in Zabbix webui

    |Key|Value|
    |:--|:--|
    |Name|Slack|
    |Type|Script|
    |Script name|slack|
    |Script parameters 1|{ALERT.SENDTO}
    |Script parameters 2|{ALERT.SUBJECT}
    |Script parameters 3|{ALERT.MESSAGE}|
    |Enabled|x|

    `Script parameters` is from Zabbix3

1. Users -> select user -> Media -> Add

    |Key|Value|
    |:--|:--|
    |Type|Slack|
    |Send to|Webhook url(get above)|
    |Enabled|x|

### 4. Create action
1. Configuration -> Actions -> Create action
    * Action  
        Information you want in alert. Each lines are as `KEY: VALUE`

        e.g.)
        ```
        DATETIME: {DATE} {TIME}
        TRIGGER_STATUS: {TRIGGER.STATUS}
        TRIGGER_SEVERITY: {TRIGGER.SEVERITY}
        HOST: {HOST.HOST1}
        TRIGGER: {TRIGGER.NAME}
        ITEM_NAME: {ITEM.NAME1}
        ITEM_KEY: {ITEM.KEY1}
        ITEM_VALUE: {ITEM.VALUE1}
        ```

        ***This script needs `DATETIME`, `TRIGGER_STATUS` and `TRIGGE_SERVERITY` lines***

    * Operatins  
        Add an operation, in which you should choose a media `Slack`.

### Done!
