FROM alpine

MAINTAINER hhx7 

ENV AZK_VERSION 3.57.0
ENV MYSQL_JDBC_VERSION 5.1.35
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV HADOOP_VERSION 3.1.3
ENV HADOOP_HOME /hadoop-${HADOOP_VERSION}
ENV HIVE_VERSION 3.1.2
ENV HIVE_HOME /apache-hive-${HIVE_VERSION}-bin
ENV PATH $JAVA_HOME/bin:$HIVE_HOME/bin:$HADOOP_HOME/bin:$PATH

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories
RUN apk add --update openjdk8-jre curl bash mysql-client python2 tar && rm -rf /var/cache/apk/* && mkdir app && mkdir app/logs

COPY ./azkaban-exec-server-0.1.0-SNAPSHOT app/
# Work around to run container as a daemon
#RUN sed -i "s/&//" /app/bin/start-exec.sh
#RUN sed -i "s/&//" /app/bin/internal/internal-start-executor.sh

#Hadoop Hive Environment
ADD https://mirror.bit.edu.cn/apache/hadoop/common/current/hadoop-${HADOOP_VERSION}.tar.gz /hadoop
ADD https://mirror.bit.edu.cn/apache/hive/hive-${HIVE_VERSION}/apache-hive-${HIVE_VERSION}-bin.tar.gz /hive
#ADD hadoop-${HADOOP_VERSION}.tar.gz /hadoop
#ADD apache-hive-${HIVE_VERSION}-bin.tar.gz /hive



RUN tar -zxf /hive && tar -zxf /hadoop && rm -f /hadoop && rm -f /hive && rm ${HIVE_HOME}/lib/guava-*.jar && cp ${HADOOP_HOME}/share/hadoop/common/lib/guava*.jar ${HIVE_HOME}/lib/


# Azkaban web server port
EXPOSE 12321

# Define default workdir
WORKDIR /app
RUN chmod +x ./bin/*.sh

CMD ["./bin/run.sh"]
