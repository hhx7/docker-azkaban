FROM alpine

MAINTAINER hhx7 

ENV AZK_VERSION 3.57.0
ENV MYSQL_JDBC_VERSION 5.1.35

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories
RUN apk add --update openjdk8-jre curl bash mysql-client python2 && rm -rf /var/cache/apk/* && mkdir app && mkdir app/logs

COPY ./azkaban-exec-server-0.1.0-SNAPSHOT app/
# Work around to run container as a daemon
#RUN sed -i "s/&//" /app/bin/start-exec.sh
#RUN sed -i "s/&//" /app/bin/internal/internal-start-executor.sh
# Azkaban web server port
EXPOSE 12321

# Define default workdir
WORKDIR /app
RUN chmod +x ./bin/*.sh

CMD ["./bin/run.sh"]
