# Ansible Kafka Cluster
Ansible to install and configure a Kafka cluster

### Install
Start ansible script
```
ansible-playbook -i hosts site.yml -f 3
```

### Test 

To test the cluster try to create a topic and then to produce/consume some messages.

So log into one of the node and create a topic:

```bash
$ {{ kafka_location }}/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 10 --topic test

$ {{ kafka_location }}/bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic test
```

Then, log into an other node a start consuming from this topic:

```bash
$ {{ kafka_location }}/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic test
```

Finally, log into an other node and start produce messages in this topic:

```bash
$ {{ kafka_location }}/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

Note: This tests can be done on the same node, using different shells, but in this way we test also the connection between the clusters
