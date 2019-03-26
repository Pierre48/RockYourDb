# Rock your database
---
## What ?
![alt text](assets/oracle.gif "Oracle")
![alt text](assets/debezium.png "Debezium")
![alt text](assets/kafka.png "Kafka")
---
# Kafka installation
+++
## Kafka download
https://www.apache.org/dyn/closer.cgi?path=/kafka/2.1.0/kafka_2.11-2.1.0.tgz
+++
## Unzip it
~~~~
tar -xzf kafka_2.11-2.1.0.tgz
cd kafka_2.11-2.1.0
~~~~
+++
### Start a ZooKeeper
~~~~
.\bin\windows\zookeeper-server-start.bat config\zookeeper.properties
~~~~
+++
### Start a Kafka server
~~~~
.\bin\windows\kafka-server-start config/server.properties
~~~~
+++
---
# Create a basic publisher
+++
## Create a console application
~~~~ 
cd src
dotnet new console -n publisher
cd publisher
dotnet add package -v 1.0.0-RC1 Confluent.Kafka'
~~~~ 
+++
## Add code for publication
~~~~ 
            var config = new ProducerConfig { BootstrapServers = "localhost:9092" };
            using (var p = new ProducerBuilder<Null, string>(config).Build())
            {
                try
                {   
                    var dr =  p.Produce("test-topic", new Message<Null, string> { Value = "test" });
                }
                catch (ProduceException<Null, string> e)
                {
                    Console.WriteLine($"Delivery failed: {e.Error.Reason}");
                }
            }
~~~~ 
+++