# Rock your database
---
## What ?
![alt text](assets/oracle.gif "Oracle")
![alt text](assets/debezium.png "Debezium")
![alt text](assets/kafka.png "Kafka")
---
++++
# Kafka installation
---
## Kafka download
https://kafka.apache.org/quickstart
+++
# Create a basic publisher
---
## Create a console application
~~~~ 
cd src
dotnet new console -n publisher
cd publisher
dotnet add package -v 1.0.0-RC1 Confluent.Kafka'
~~~~ 
---
## Add code for publication
~~~~ 
        var config = new ProducerConfig { BootstrapServers = "localhost:9092" };

        // If serializers are not specified, default serializers from
        // `Confluent.Kafka.Serializers` will be automatically used where
        // available. Note: by default strings are encoded as UTF8.
        using (var p = new ProducerBuilder<Null, string>(config).Build())
        {
            try
            {
                var dr = await p.ProduceAsync("test-topic", new Message<Null, string> { Value="test" });
                Console.WriteLine($"Delivered '{dr.Value}' to '{dr.TopicPartitionOffset}'");
            }
            catch (ProduceException<Null, string> e)
            {
                Console.WriteLine($"Delivery failed: {e.Error.Reason}");
            }
        }
~~~~ 
