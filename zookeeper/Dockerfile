FROM java:openjdk-8-jre
MAINTAINER Abhishek Jalan <abhishek.jalan84@gmail.com>

# The used ZooKeeper version can also be supplied like this with the build command like this:
# --build-arg BIN_VERSION=zookeeper-3.4.14
ARG BIN_VERSION=zookeeper-3.4.14

WORKDIR /usr/share/zookeeper

EXPOSE 2181 2888 3888

# Install and set everything up
RUN echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list
RUN sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list
RUN apt-get -o Acquire::Check-Valid-Until=false update -y
RUN apt-get install -y apt-utils
RUN apt-get install -y wget tar vim
RUN mkdir /var/lib/zookeeper
RUN mkdir /var/log/zookeper
RUN \
   wget -q -N http://mirror.dkd.de/apache/zookeeper/$BIN_VERSION/$BIN_VERSION.tar.gz \
&& tar --strip-components=1 -C /usr/share/zookeeper -xvf ${BIN_VERSION}.tar.gz \
&& rm $BIN_VERSION.tar.gz \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

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
