FROM --platform=linux/arm64 eclipse-temurin:17-jdk-jammy

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl ca-certificates procps python3 && \
    rm -rf /var/lib/apt/lists/*

RUN curl -fSL \
    https://dlcdn.apache.org/hadoop/common/hadoop-3.5.0/hadoop-3.5.0-aarch64.tar.gz \
    -o /tmp/hadoop.tar.gz && \
    tar -xzf /tmp/hadoop.tar.gz -C /opt && \
    mv /opt/hadoop-3.5.0 /opt/hadoop && \
    rm /tmp/hadoop.tar.gz

ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CONF_DIR=/opt/hadoop/etc/hadoop
ENV PATH="/opt/hadoop/bin:/opt/hadoop/sbin:${PATH}"

CMD ["sleep", "infinity"]
