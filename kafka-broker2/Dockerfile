FROM nimmis/java-centos:openjdk-7-jdk
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 2.3.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka and other needed things
RUN yum install epel-release -y
RUN yum update -y
RUN mkdir /var/log/kafkabroker
RUN yum install -y wget vim dnsutils net-tools && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q http://mirror.dkd.de/apache/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

RUN sed -i -e '/^log\.dirs=\/tmp\/kafka-logs/s/^.*$/log\.dirs=\/var\/log\/kafkabroker/g' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties

RUN sed -i '22 i port=9093' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties


ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh
RUN chmod +x /usr/bin/start-kafka.sh

EXPOSE 9093

ENTRYPOINT ["/usr/bin/start-kafka.sh"]
