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