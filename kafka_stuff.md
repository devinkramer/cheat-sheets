## Useful Links
http://www.slideshare.net/miguno/apache-kafka-08-basic-training-verisign
http://research.microsoft.com/en-us/um/people/srikanth/netdb11/netdb11papers/netdb11-final12.pdf
http://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying
http://engineering.linkedin.com/kafka/intra-cluster-replication-apache-kafka
http://kafka.apache.org/documentation.html#design
http://www.hakkalabs.co/articles/site-reliability-engineering-linkedin-kafka-service
http://grokbase.com/t/kafka/users/145qtx4z1c/topic-partitioning-strategy-for-large-data
https://cwiki.apache.org/confluence/display/KAFKA/System+Tools
https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-HowdoIchoosethenumberofpartitionsforatopic?

# v0.9 and earlier Zookeeper managed Consumer Offsets
## List Consumer Groups
```bash
/usr/lcal/kafka/bin/kafka-consumer-groups.sh --zookeeper $ZOO:2181 --list
```
## Pull Offsets for a speicfic ConsumerGroup
```bash
/usr/local/kafka/bin/kafka-run-class.sh kafka.tools.ConsumerOffsetChecker --zookeeper $ZOO:2181 --group [group id]
```

# v0.10+ using broker __consumer_offset topic
## List Consumer Groups
```bash
/usr/local/kafka/bin/kafka-consumer-groups.sh --bootstrap-server $BROKER:9092  --list
```
## Details about a group
```bash
/usr/local/kafka/bin/kafka-consumer-groups.sh --bootstrap-server $BROKER:9092  --describe --group $GROUP
```
## Get Earliest offsets for a topic 
```bash
/usr/local/kafka/bin/kafka-run-class.sh  kafka.tools.GetOffsetShell --broker-list $BROKER:9092 --topic $TOPIC_NAME --time -2 | $TOPIC_NAME:$PARTITION_NUM
```
## Get Latest offset for a topic
```bash
/usr/local/kafka/bin/kafka-run-class.sh  kafka.tools.GetOffsetShell --broker-list $BROKER:9092 --topic $TOPIC_NAME --time -1 | grep $TOPIC_NAME:$PARTITI
ON_NUM
```
```
