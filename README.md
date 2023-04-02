
# Apache Kafka - Linux CentOS 7 Installation

#### STEP 1: Update sudo
```bash
sudo yum update -y && sudo reboot
```

#### STEP 2: Install OpenJDK Runtime
```bash
	sudo yum install java-1.8.0-openjdk.x86_64
```
2.2. Validate your installation
```bash
	java -version
```
The output should resemble:

	openjdk version "1.8.0_91"
	OpenJDK Runtime Environment (build 1.8.0_91-b14)
	OpenJDK 64-Bit Server VM (build 25.91-b14, mixed mode)

2.3. You need JVM (Java Virtual Machine) and Java Runtime Environment (JRE) for Zookeeper

Open "profile" file
	
    /etc/profile 

Add these lines to defide JVM and JRE

	export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk
	export JRE_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.362.b08-1.el7_9.x86_64/jre

2.4. Reload the profile
```bash   
     source /etc/profile
```

#### STEP 3: Download Apache Kafka

3.1 Go to "opt" folder
```bash 
	cd /opt/
```
3.2 Download Kafka in to "opt" folder
```bash 
	wget http://www-us.apache.org/dist/kafka/0.9.0.1/kafka_2.11-0.9.0.1.tgz
```
3.3. Unzip
```bash 
	tar -xvf kafka_2.11-0.9.0.1.tgz
```
3.4. Change "kafka_2.11-0.9.0.1" folder name to "kafka"


#### STEP 4: Start and test Apache Kafka

Zookeeper comes with Kafka version 2. You dont need extra install 

4.1. Start the Zookeeper server 
```bash 
	bin/zookeeper-server-start.sh -daemon config/zookeeper.properties
```

4.2. Modify the configuration of your Kafka server

	Open with editor "/opt/bin/kafka-server-start.sh" file

4.3. Adjust the memory usage according to your specific system parameters.
	
Find
    
    export KAFKA_HEAP_OPTS="-Xmx1G -Xms1G"

Replace with
	
    export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"

4.4. Start the Kafka server

Open a new terminal

```bash
	cd /opt/kafka
```

```bash
	bin/kafka-server-start.sh config/server.properties
```
How can i understand Kafta start?
	
    You will see in teminal "INFO [KafkaServer id=0] started (kafka.server.KafkaServer)" and wait

#### 5. TEST KAFKA

5.1. create topic as "test-topic"
	
Open teminal
```bash
	cd /opt/kafka
```
```bash
	bin/kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092 --replication-factor 1 --partitions 4
```

5.2 List of topics
Open teminal
```bash
	cd /opt/kafka
```
```bash
	bin/kafka-topics.sh --bootstrap-server=localhost:9092 --list
```	
5.3. Produce message for topic "test-topic"
Open teminal
```bash
	cd /opt/kafka
```
```bash
	bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic
	type your message
```	
5.3. Display message
Open teminal
```bash
	cd /opt/kafka
```
```bash
	bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test-topic --from-beginning
```
    You will see messages in "test-topic" 




