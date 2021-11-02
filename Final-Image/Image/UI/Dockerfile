#Base Image
FROM hpro99/test:ui-newv1 as build

#New Base for reduce size
FROM alpine

#Copy file from base
COPY --from=build /start.sh /
RUN sed -i '$s/exec//g' /start.sh  
COPY --from=build /opt/apache-storm /opt/

#Install OpenJDK11 & Bash
RUN apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community && apk update && apk add bash

#Export Variable for Storm
ENV PATH "$PATH:/opt/apache-storm-2.2.0/bin"
WORKDIR /opt/apache-storm-2.2.0

#Install Python
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip && pip3 install --no-cache --upgrade pip setuptools

#Expose port for UI
EXPOSE 8080

#RUn 
ENTRYPOINT ["/start.sh"]
