# HBase + ElasticSearch + Kafka Setup Using Docker

This configuration builds an HBase, ElasticSearch and Kafka setup in a Docker topology. HBase and Kafka are built from Dockerfiles, while Elasticsearch (and the supporting Zookeeper for Kafka) are built using the official images.

## Building

    $ git clone https://github.com/jamesattard/hbase-es-kafka
    $ cd hbase-es-kafka/
    $ docker-compose build

## Run the HBase-ES-Kafka Cluster

    $ docker-compose up
