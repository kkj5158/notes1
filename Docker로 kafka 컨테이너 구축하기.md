#DevOps 

이번에는, docker와 docker-compose를 사용해서 kafka 컨테이너를 구축해보자. 

compose yml 파일을 다음과 같이 작성하자. 

```shell
version: '3.7'

services:

  # zookeeper

  zookeeper:

    image: wurstmeister/zookeeper

    container_name: zookeeper

    ports:

      - "2181:2181"

  # kafka

  # kafka:

  #   image: wurstmeister/kafka

  #   container_name: kafka

  #   ports:

  #     - "9092:9092"

  #   environment:

  #     KAFKA_ADVERTISED_HOST_NAME: 127.0.0.1

  #     KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181

  #   volumes:

  #     - /var/run/docker.sock:/var/run/docker.sock

  kafka1:

    hostname: kafka1

    image: wurstmeister/kafka

    container_name: kafka1

    ports:

      - "9092:9092"

    environment:

      KAFKA_LISTENERS: LISTENER_DOCKER_INTERNAL://:19092,LISTENER_DOCKER_EXTERNAL://:9092

      KAFKA_ADVERTISED_LISTENERS: LISTENER_DOCKER_INTERNAL://kafka1:19092,LISTENER_DOCKER_EXTERNAL://3.38.35.127:9092

      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_DOCKER_INTERNAL:PLAINTEXT,LISTENER_DOCKER_EXTERNAL:PLAINTEXT

      KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_DOCKER_INTERNAL

      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"

      KAFKA_BROKER_ID: 1

      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 3

    volumes:

      - /var/run/docker.sock:/var/run/docker.sock

      - /config/kafka-server-start.sh:/opt/kafka/bin/kafka-server-start.sh:ro,Z

    depends_on:

      - zookeeper

  kafka2:

    hostname: kafka2

    image: wurstmeister/kafka

    container_name: kafka2

    ports:

      - "9093:9093"

    environment:

      KAFKA_LISTENERS: LISTENER_DOCKER_INTERNAL://:19093,LISTENER_DOCKER_EXTERNAL://:9093

      KAFKA_ADVERTISED_LISTENERS: LISTENER_DOCKER_INTERNAL://kafka2:19093,LISTENER_DOCKER_EXTERNAL://3.38.35.127:9093

      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_DOCKER_INTERNAL:PLAINTEXT,LISTENER_DOCKER_EXTERNAL:PLAINTEXT

      KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_DOCKER_INTERNAL

      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"

      KAFKA_BROKER_ID: 2

      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 3

    volumes:

      - /var/run/docker.sock:/var/run/docker.sock

      - /config/kafka-server-start.sh:/opt/kafka/bin/kafka-server-start.sh:ro,Z

    depends_on:

      - zookeeper
```

해당 스크립트는 카프카컨테이너 2개와 이를 관리하는 zookeeper 1대를 구성하여서 컨테이너를 관리하게끔 만들어준다. 