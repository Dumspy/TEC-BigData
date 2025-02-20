FROM debian:12

# # MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>
# # MAINTAINER Giannis Mouchakis <gmouchakis@iit.demokritos.gr>

LABEL maintainer="Robert C. Green II <greenr@bgsu.edu>"

# RUN apt-get update && apt-get install -y python3 python3-pip && rm -rf /var/lib/apt/lists/*
# RUN pip3 install hdfs
RUN apt-get update 
RUN  apt-get install -y --no-install-recommends default-jdk 
RUN  apt-get install -y --no-install-recommends net-tools 
RUN  apt-get install -y --no-install-recommends curl 
# RUN  apt-get install -y --no-install-recommends netcat 
RUN  apt-get install -y --no-install-recommends gnupg 
RUN  apt-get install -y --no-install-recommends libsnappy-dev 
RUN apt-get install -y python3 python3-setuptools python3-pip python3-venv
RUN rm -rf /var/lib/apt/lists/*
      
# RUN pip3 install -U hdfs mrjob
# RUN apt-get install -y python3-hdfs python3-mrjob
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64/

RUN curl -O https://dist.apache.org/repos/dist/release/hadoop/common/KEYS

RUN gpg --import KEYS

ENV HADOOP_VERSION=3.4.1
ENV HADOOP_URL=https://www.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz

RUN set -x \
    && curl -fSL "$HADOOP_URL" -o /tmp/hadoop.tar.gz \
    && curl -fSL "$HADOOP_URL.asc" -o /tmp/hadoop.tar.gz.asc \
    && gpg --verify /tmp/hadoop.tar.gz.asc \
    && tar -xvf /tmp/hadoop.tar.gz -C /opt/ \
    && rm /tmp/hadoop.tar.gz*

RUN ln -s /opt/hadoop-$HADOOP_VERSION/etc/hadoop /etc/hadoop

RUN mkdir /opt/hadoop-$HADOOP_VERSION/logs

RUN mkdir /hadoop-data

ENV HADOOP_HOME=/opt/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR=/etc/hadoop
ENV MULTIHOMED_NETWORK=1
ENV USER=root
ENV PATH=$HADOOP_HOME/bin/:$PATH

ADD entrypoint.sh /entrypoint.sh

RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]