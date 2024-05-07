##### Setup Kafka in Docker 

## Create a Docker network:
for the Kafka setup to allow communication between containers:

docker network create kafka-net 

## Start Zookeeper:
Zookeeper is a prerequisite for running Kafka, as it manages the state and configuration of the Kafka cluster. Start a Zookeeper container using the Confluent Docker image

docker run -d --name zookeeper --network kafka-net -p 2181:2181 -e ALLOW_ANONYMOUS_LOGIN=yes bitnami/zookeeper

## Start Kafka:
docker run -d --name kafka --network kafka-net  -p 9092:9092  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181  -e ALLOW_PLAINTEXT_LISTENER=yes  bitnami/kafka 

## create a topic:
docker exec -it kafka kafka-topics.sh --create --topic ismail-topic --bootstrap-server localhost:9092

Have a two terminal and execute each message in each tab and send message in the producer tab and it will be reflected in the second consumer tab

## produce messages:
docker exec -it kafka kafka-console-producer.sh --topic ismail-topic --bootstrap-server localhost:9092
give ctrl + C to close it

## Consume messages:
docker exec -it kafka kafka-console-consumer.sh --topic ismail-topic --bootstrap-server localhost:9092 --from-beginning
give ctrl + C to close it





