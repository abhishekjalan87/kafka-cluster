FROM centos:7
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 2.3.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka and other needed things
RUN yum install epel-release -y
RUN yum update -y
RUN mkdir /var/log/kafkabroker
RUN yum install java-1.8.0-openjdk.x86_64 wget vim dnsutils net-tools -y && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q http://mirror.dkd.de/apache/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

RUN yum clean all
RUN sed -i -e '/^log\.dirs=\/tmp\/kafka-logs/s/^.*$/log\.dirs=\/var\/log\/kafkabroker/g' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties

RUN sed -i '22 i port=9092' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties

RUN sed -i '24 i advertised.listeners=PLAINTEXT://kafkabroker1:9092' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties


ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh
RUN chmod +x /usr/bin/start-kafka.sh

EXPOSE 9092

ENTRYPOINT ["/usr/bin/start-kafka.sh"]
