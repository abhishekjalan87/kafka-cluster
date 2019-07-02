FROM java:openjdk-8-jre
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 2.3.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka and other needed things
RUN echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list
RUN sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list
RUN apt-get -o Acquire::Check-Valid-Until=false update -y
RUN apt-get install -y apt-utils
RUN mkdir /var/log/kafkabroker
RUN apt-get install -y wget vim dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    wget -q http://mirror.dkd.de/apache/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

RUN sed -i -e '/^log\.dirs=\/tmp\/kafka-logs/s/^.*$/log\.dirs=\/var\/log\/kafkabroker/g' /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/config/server.properties

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh
RUN chmod +x /usr/bin/start-kafka.sh

EXPOSE 9092

ENTRYPOINT ["/usr/bin/start-kafka.sh"]
