#Base Image
FROM hpro99/test:workerv1 as build

#New Base for reduce size
FROM alpine

#Copy file from base
COPY --from=build /start.sh /
RUN sed -i '$s/exec//g' /start.sh
RUN chmod +x /start.sh
COPY --from=build /opt/apache-storm /opt/

#Install OpenJDK11 & Bash
RUN apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community
RUN  apk update && apk add bash

#Export Variable for Storm
ENV PATH "$PATH:/opt/apache-storm-2.2.0/bin"
WORKDIR /opt/apache-storm-2.2.0

#Reconfig storm.yaml
RUN echo "topology.eventlogger.executors: 1" >> conf/storm.yaml
RUN echo worker.childopts: \"-Xmx%HEAP-MEM%m -Xlog:gc*:artifacts/gc.log:time,uptime,level,tags:filecount=10,filesize=1M -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=artifacts/heapdump\" >> conf/storm.yaml

RUN cat conf/storm.yaml | taln -n 5
#Install Python
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools

#Expose port for UI
EXPOSE 6700 6701 6702 6703 

#RUn 
ENTRYPOINT ["/start.sh"]
