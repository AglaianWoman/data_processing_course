FROM openjdk:8-jdk-slim
LABEL maintainer="Luis Belloch <docker@luisbelloch.es>"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3-software-properties python3-numpy curl && \
    rm -rf /var/lib/apt/lists/*

ENV SPARK_HOME=/opt/spark
RUN mkdir -p /opt/spark && curl -s http://apache.rediris.es/spark/spark-2.2.1/spark-2.2.1-bin-hadoop2.7.tgz | tar -xz -C "${SPARK_HOME}" --strip-components=1
ENV PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH

RUN curl -s -o $SPARK_HOME/jars/hadoop-aws-2.7.3.jar https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.3/hadoop-aws-2.7.3.jar && \
    curl -s -o $SPARK_HOME/jars/aws-java-sdk-1.7.4.jar http://central.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar

COPY conf/spark-defaults.conf $SPARK_HOME/conf

ENV SPARK_NO_DAEMONIZE=true
ENV PYSPARK_PYTHON=python3
EXPOSE 4040 7077 8080

CMD ["pyspark"]

