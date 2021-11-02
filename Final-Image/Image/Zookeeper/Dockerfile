#Base Image
FROM hpro99/zookeeper:1.0 as build

#New Base for reduce size
FROM alpine

#Copy file from base
COPY --from=build /opt/zookeeper /opt/

#Install OpenJDK11 & Bash
RUN apk update &&  apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community && apk add bash

#Export Variable for Storm
WORKDIR /opt/apache-zookeeper-3.6.3-bin

#Install Python

#Expose port for UI
EXPOSE 2181 2888 3888 8888

#RUn
ENTRYPOINT ["/opt/apache-zookeeper-3.6.3-bin/bin/zkServer.sh"]
CMD ["start-foreground"] 
