FROM centos:7
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

# The used ZooKeeper version can also be supplied like this with the build command like this:
# --build-arg BIN_VERSION=zookeeper-3.4.14
ARG BIN_VERSION=zookeeper-3.4.14
ARG APACHE_NAME=zookeeper-3.4.14

WORKDIR /usr/share/zookeeper

EXPOSE 2181 2888 3888

# Install and set everything up
RUN yum install epel-release -y
RUN yum update -y
RUN yum install wget java-1.8.0-openjdk tar dnsutils vim net-tools -y
RUN mkdir /var/lib/zookeeper
RUN mkdir /var/log/zookeper
RUN \
   wget -q -N http://mirror.dkd.de/apache/zookeeper/$BIN_VERSION/$APACHE_NAME.tar.gz \
&& tar --strip-components=1 -C /usr/share/zookeeper -xvf ${APACHE_NAME}.tar.gz \
&& rm $APACHE_NAME.tar.gz \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN yum clean all

# default parameters for config file:
ENV tickTime=2000
ENV dataDir=/var/lib/zookeeper/
ENV dataLogDir=/var/log/zookeeper/
ENV clientPort=2181
ENV initLimit=5
ENV syncLimit=2

# add startup script
ADD entrypoint.sh entrypoint.sh
RUN chmod +x entrypoint.sh

ENTRYPOINT ["/usr/share/zookeeper/entrypoint.sh"]
