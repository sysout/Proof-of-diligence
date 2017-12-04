## zookeeper stat
telnet localhost 2181

## create a topic
bin/kafka-topics.sh --create --topic my_topic --zookeeper localhost:2181 --replication-factor 1 --partitions 1

## list topics
bin/kafka-topics.sh --list --zookeeper localhost:2181

## produce messages
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my_topic

## consume messages about a topic
bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic my_topic --from-beginning

## tmp/kafka-log
ls /tmp/kafka-logs/my_topic-0/

## consumer group.id
Consumers label themselves with a consumer group name, and each record published to a topic is delivered to one consumer instance within each subscribing consumer group. Consumer instances can be in separate processes or on separate machines.

If all the consumer instances have the same consumer group, then the records will effectively be load balanced over the consumer instances.

If all the consumer instances have different consumer groups, then each record will be broadcast to all the consumer processes.
