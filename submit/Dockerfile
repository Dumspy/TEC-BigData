# FROM bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8

# MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>

COPY WordCount.jar /opt/hadoop/applications/WordCount.jar


FROM rgreen13/hadoop-base:latest
LABEL maintainer="Robert C. Green II <greenr@bgsu.edu>"

ENV JAR_FILEPATH="/opt/hadoop/applications/WordCount.jar"
ENV CLASS_TO_RUN="WordCount"
ENV PARAMS="/input /output"

ADD run.sh /run.sh
RUN chmod a+x /run.sh

CMD ["/run.sh"]
