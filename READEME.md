# AWX Configuration as Code
This repository is to allow my instance of AWX to get the benefits of version control. Having config as code also allows me to quickly standup AWX with my configs in the event of requiring a full redeployment.

## Preparing Installation of the Configurations
You will need to create 2 files in a directory named **vars/**.
1. ssh_private_key.pem
1. vars.yml (with the below contents and values to suit your requirements)
```yml
TOWER_HOST:
TOWER_USERNAME:
TOWER_PASSWORD:

POSTGRES_HOST:
POSTGRES_USERNAME:
POSTGRES_PASSWORD:
POSTGRES_DB_NAME:

SPLUNK_URL:
SPLUNK_HEADER:
SPLUNK_HEADER_02:

ENCRYPTION_KEY_ID:
BASE_API:
LOGIN_URL:
B_USERNAME:
B_PASSWORD:
B_USERNAME_02:
B_PASSWORD_02:

BANK:
DAYS_AGO:

GET_TRANSACTIONS_PLAYBOOK:
CREDENTIAL_GET_TRANSACTIONS_01:
CREDENTIAL_GET_TRANSACTIONS_02:
CRENDENTIAL_TYPE_GET_TRANSACTIONS:
CREDENTIAL_SPLUNK_HEC_01:
CREDENTIAL_SPLUNK_HEC_02:
USER_02:

WORKFLOW_VARS:
  - WORKFLOW_NAME:
    TRANSACTION_TYPE:
    ACCOUNT_NAME:
    TABLE_NAME:
    GET_IB_DATA_TEMPLATE_NAME:
    SEND_TO_SPUNK_TEMPLATE_NAME:
    START_HOUR:
    START_MINUTE:
    RRULES:
      - frequency: "week"
        interval: 2
        byweekday: "tuesday,wednesday"
        include: True

  - WORKFLOW_NAME:
    TRANSACTION_TYPE:
    ACCOUNT_NAME:
    TABLE_NAME:
    GET_IB_DATA_TEMPLATE_NAME:
    SEND_TO_SPUNK_TEMPLATE_NAME:
    START_MINUTE:
    RRULES:
      - frequency: "hour"
        interval: 3

GIT_USERNAME:
GIT_PRIVATE_KEY:
GIT_PRIVATE_KEY_PHRASE:
GIT_SCM_URL:
GIT_SCM_BRANCH:
```

You will also need to install pip modules required by rrules for scheduling workflow templates.
* pytz
* python-dateutil

### How to use ansible vault
I recommend encrypting **vars.yml**. I have done so by using `ansible-vault`.

`ansible-vault <command> vars.yml`
1. encrypt 
1. view 
1. edit
1. decrypt


## Installing the Configurations

Run **main.yml** playbook to install the configuraions.

`ansible-playbook tasks/main.yml --ask-vault-pass`

## Useful Documentation
* https://galaxy.ansible.com/awx/awx?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW
* https://docs.ansible.com/ansible/devel/collections/awx/awx/index.html
* https://dateutil.readthedocs.io/en/stable/rrule.html
* https://python.hotexamples.com/examples/dateutil.rrule/-/rrule/python-rrule-function-examples.html
