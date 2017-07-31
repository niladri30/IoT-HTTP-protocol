# IoT-HTTP-protocol
Scala based HTTP Protocol Adapter for IoT Ingestion Layer

In IoT platform setting up the space using less foot-print in ingestion layers is a great way to build the complete platform. There are various ways to have a light weight Rest service, which can be used for HTTP protocol layer. This layer will communicate over TCP layer.
As HTTP is one of the protocol which is used for communication via Gateways, so keeping it light-weighted and error free is much more needed.

Simple workflow for HTTP protocol in IoT Platform

Data(JSON/CSV) from sensor  ----> HTTP Protocol Adapter(POST-Finatra) ----> Kafka Cluster

This HTTP Adapter is build upon Finatra (https://github.com/twitter/finatra). I started with building usual Rest services using Java and Scala. After lot of research and POCs I stick to this service, as I found the messages transferred via this adapter is having zero-error and more tps value.

This project is used with Kafka, so as soon as the message comes in.. it get transferred to Kafka topics. We have used Kafka cluster (3 node) to get the data in a single topic. Transferring the message via HTTP without any message loss was a great challenge, which I tried to solve it. 

Our Jmeter Test results:
------
1. Messages got transferred using Java and Tomcat -> 20K - 24K TPS (after tunning tomcat) without errors.
2. Messages got transferred using Scala and Akka -> 18K TPS with errors.
3. Messages got transferred using Scala and Finatra -> 45K TPS without errors and still rising.

This project is easy to deploy and has implemented Logback, reading from property files, validation for JSON and CSV message, Authentication Layer.

Steps to run:
-------
1. Provide the kafka instances for Bootstrap servers (kafka_config.properties).
2. Build the project using-> sbt
3. Once completed type -> run to start the project
4. Try to post a json message using http://localhost:8080/neel/ingest
5. Open finatra admin console on http://localhost:9990 for checking the activity for request hit


