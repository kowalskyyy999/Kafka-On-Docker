ARG KAFKA_VERSION

FROM kafka:${KAFKA_VERSION}

ENV TZ="Asia/Jakarta"

RUN apt-get install unzip -y

COPY config/connect-distributed.properties $KAFKA_HOME/config/connect-distributed.properties

COPY instantclient-basic-linux.x64-12.2.0.1.0.zip /usr/local/etc/instantclient-basic-linux.x64-12.2.0.1.0.zip

WORKDIR /usr/local/etc

RUN unzip instantclient-basic-linux.x64-12.2.0.1.0.zip
ENV LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/etc/instantclient_12_2"

RUN cp -r /usr/local/etc/instantclient_12_2 ${KAFKA_HOME}/plugins/
RUN cp /usr/local/etc/instantclient_12_2/*.jar ${KAFKA_HOME}/libs/

CMD $KAFKA_HOME/bin/connect-distributed.sh $KAFKA_HOME/config/connect-distributed.properties
