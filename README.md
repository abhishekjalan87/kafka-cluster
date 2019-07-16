# kafka-cluster
under testing



## Deploy Kafka-Zookeeper (This Zookeeper will connect both Kafka Brokers)
docker run -d --name zookeeper --restart=always -p 2181:2181 -e ALLOW_ANONYMOUS_LOGIN=yes -v /var/lib/zookeeper:/var/lib/zookeeper -v /var/log/zookeeper:/var/log/zookeeper ajalan/kafkazookeeper:latest zookeeper

## Deploy Kafka-Broker1
docker run --name kafkabroker1 -e KAFKA_HOST=kafkabroker1 -e KAFKA_PORT=9092 -v /var/log/kafkabroker:/var/log/kafkabroker -e ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ID=0  -e ALLOW_PLAINTEXT_LISTENER=yes  -p 9092:9092 ajalan/kafkabroker:latest


## Deploy Kafka-Broker2
docker run --name kafkabroker2 -e KAFKA_HOST=kafkabroker2 -e KAFKA_PORT=9093 -v /var/log/kafkabroker:/var/log/kafkabroker -e ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ID=1  -e ALLOW_PLAINTEXT_LISTENER=yes  -p 9093:9093 ajalan/kafkabroker2:latest