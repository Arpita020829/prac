# prac
------------------------------------------------
cd /workspaces/prac
wget https://dlcdn.apache.org/kafka/4.3.1/kafka_2.13-4.3.1.tgz
tar -xzf kafka_2.13-4.3.1.tgz
cd kafka_2.13-4.3.1

-------------------------------------------------
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"

bin/kafka-storage.sh format --standalone -t "$KAFKA_CLUSTER_ID" -c config/server.properties

bin/kafka-server-start.sh config/server.properties

---------------------TO INSTALL KAFKA--------------------

python -m pip install kafka-python

----THEN RUN THE FILES------------

python topic.py
python consumer.py

IN OTHER TERMINAL
cd /workspaces/prac
python Producer.py

==========================================DAG======================================================
TERMINAL 1: SETUP
pip install uv
uv venv --python 3.14
source .venv/bin/activate
export AIRFLOW_HOME=/workspaces/AIOps/airflow
mkdir -p $AIRFLOW_HOME/dags
uv pip install apache-airflow
airflow db migrate
cd $AIRFLOW_HOME/dags
touch aiops_dag.py
airflow standalone

TERMINAL 2: VERIFY AND RUN
cd /workspaces/AIOps
source .venv/bin/activate
export AIRFLOW_HOME=/workspaces/AIOps/airflow

airflow config get-value core dags_folder
airflow dags list
airflow dags list | grep aiops
airflow dags list-import-errors

airflow dags unpause aiops_workflow
airflow dags trigger aiops_workflow
airflow dags list-runs -d aiops_workflow
