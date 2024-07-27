# 🚀 Apache Kafka

This repository provides a basic setup for running Apache Kafka, a distributed streaming platform, on Windows. It includes scripts for starting ZooKeeper, Kafka Server, creating topics, and interacting with them using producers and consumers.

## Prerequisites

* **☕ Java 8 or later:** Kafka requires Java for execution. Download and install from the official Java website ([https://www.java.com/download/](https://www.java.com/download/)).
* **🖥️ Windows OS:** This guide assumes a Windows environment.

## Installation

1. **📥 Download Kafka:**
   - Visit the Apache Kafka downloads page ([https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)) and download the latest binary release for Windows.
2. **📂 Extract the archive:**
   - Extract the downloaded archive (e.g., `kafka_2.x.y-windows.tgz`) to a directory of your choice (e.g., `C:\kafka`).

## Configuration

1. **📝 Edit `zookeeper.properties`:**
   - Open the `config/zookeeper.properties` file in a text editor.
   - Ensure the `dataDir` property points to a directory for storing ZooKeeper data (e.g., `dataDir=C:\kafka-zookeeper\data`).
2. **🛠️ Edit `server.properties`:**
   - Open the `config/server.properties` file in a text editor.
   - Set the `broker.id` property to a unique identifier for each Kafka broker (e.g., `broker.id=0`).
   - Set the `listeners` property to specify the hostname or IP address and port where Kafka will listen for connections (e.g., `listeners=PLAINTEXT://localhost:9092`).
   - Adjust other properties as needed (refer to the Kafka documentation for detailed explanations).

## Running Kafka

1. **🐘 Start ZooKeeper:**
   - Open a command prompt and navigate to the Kafka bin directory (e.g., `C:\kafka\bin\windows`).
   - Run the following command:

     ```sh
     .\zookeeper-server-start.bat .\config\zookeeper.properties
     ```

   - This will start a ZooKeeper server in the background.

2. **🔧 Start Kafka Server:**
   - In the same command prompt window, run the following command:

     ```sh
     .\kafka-server-start.bat .\config\server.properties
     ```

   - This will start a Kafka broker in the background.

## Creating Topics

1. **🗂️ Create a Topic:**
   - Use the `kafka-topics.bat` script to create a topic for streaming data.
   - Run the following command, replacing `MyFirstTopic` with your desired topic name:

     ```sh
     kafka-topics.bat --create --bootstrap-server localhost:9092 --topic MyFirstTopic
     ```

   - This command creates a topic named `MyFirstTopic` with default settings (e.g., one partition, replication factor of 1).

## Producing Data

1. **📤 Produce Messages:**
   - Use the `kafka-console-producer.bat` script to send messages to a topic.
   - Run the following command, replacing `MyFirstTopic` with your topic name:

     ```sh
     kafka-console-producer.bat --broker-list localhost:9092 --topic MyFirstTopic
     ```

   - This starts a producer prompt. Type in messages and press Enter to send them to the `MyFirstTopic` topic.

## Consuming Data

1. **📥 Consume Messages:**
   - Use the `kafka-console-consumer.bat` script to consume messages from a topic.
   - Run the following command, replacing `MyFirstTopic` with your topic name:

     ```sh
     kafka-console-consumer.bat --topic MyFirstTopic --bootstrap-server localhost:9092 --from-beginning
     ```

   - This starts a consumer that will read and print messages from the `MyFirstTopic` topic, starting from the beginning (oldest messages).

## Commands Overview

Here are all the commands consolidated for easy reference:

```sh
# 🐘 Start ZooKeeper
C:\kafka>.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

# 🔧 Start Kafka Server
C:\kafka>.\bin\windows\kafka-server-start.bat .\config\server.properties

# 🗂️ Create a Kafka Topic
C:\kafka\bin\windows>kafka-topics.bat --create --bootstrap-server localhost:9092 --topic MyFirstTopic

# 📤 Start a Kafka Producer
C:\kafka\bin\windows>kafka-console-producer.bat --broker-list localhost:9092 --topic MyFirstTopic

# 📥 Start a Kafka Consumer
C:\kafka\bin\windows>kafka-console-consumer.bat --topic MyFirstTopic --bootstrap-server localhost:9092 --from-beginning

# 📝 Describe Kafka Topic
C:\kafka\bin\windows>kafka-topics.bat --bootstrap-server localhost:9092 --describe --topic MyFirstTopic
