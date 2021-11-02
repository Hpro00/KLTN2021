#Base Image
FROM hpro99/test:nimbusv1 as build

#New Base for reduce size
FROM alpine

#Copy file from base
COPY --from=build /start.sh /
COPY --from=build /opt/apache-storm /opt/

#Install OpenJDK11 & Bash & Python
RUN apk update &&  apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community && apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python && apk add bash

#Export Variable for Storm
ENV PATH "$PATH:/opt/apache-storm-2.2.0/bin" && PYTHONUNBUFFERED=1
WORKDIR /opt/apache-storm-2.2.0

#Config  Python Pip
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools

# Reconfig storm.yaml
RUN echo "topology.eventlogger.executors: 1" >> conf/storm.yaml

#Expose port for UI
EXPOSE 3772 6627

#RUn 
ENTRYPOINT ["/start.sh"]
