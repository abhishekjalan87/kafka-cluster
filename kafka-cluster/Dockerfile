FROM java:openjdk-8-jre
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 2.2.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka and other needed things
# RUN apt-get update
RUN apt-get install -y wget && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    wget -q http://mirror.dkd.de/apache/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh
RUN chmod +x /usr/bin/start-kafka.sh

EXPOSE 9092

ENTRYPOINT ["/usr/bin/start-kafka.sh"]
