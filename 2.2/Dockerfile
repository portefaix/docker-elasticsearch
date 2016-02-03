# VERSION 2.2.0
# AUTHOR:         Nicolas Lamirault <nicolas.lamirault@gmail.com>
# DESCRIPTION:    portefaix/elasticsearch

FROM portefaix/base:3.3
MAINTAINER Nicolas Lamirault <nicolas.lamirault@gmail.com>

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=45 \
    JAVA_BUILD=14 \
    JAVA_HOME=/opt/jdk

ENV ES_VERSION 2.2.0

RUN apk add --update wget curl ca-certificates

# Install glibc
RUN cd /tmp && \
    wget "https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk" && \
    apk add --allow-untrusted glibc-2.21-r2.apk && \
    wget "https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-bin-2.21-r2.apk" && \
    apk add --allow-untrusted glibc-bin-2.21-r2.apk && \
    /usr/glibc/usr/bin/ldconfig /lib /usr/glibc/usr/lib

# Install Oracle Java
RUN cd /tmp && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
    "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    tar xzf "jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    mkdir -p /usr/lib/jvm && \
    mv "/tmp/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}" "/usr/lib/jvm/java-${JAVA_VERSION}-oracle" && \
    ln -s "java-${JAVA_VERSION}-oracle" /usr/lib/jvm/default-jvm && \
    ln -s /usr/lib/jvm/default-jvm/bin/java /usr/bin/java && \
    ln -s /usr/lib/jvm/default-jvm/bin/javac /usr/bin/javac && \
    rm -rf $JAVA_HOME/*src.zip && \
    rm -rf /usr/lib/jvm/default-jvm/*src.zip \
           /usr/lib/jvm/default-jvm/lib/missioncontrol \
           /usr/lib/jvm/default-jvm/lib/visualvm \
           /usr/lib/jvm/default-jvm/lib/*javafx* \
           /usr/lib/jvm/default-jvm/jre/lib/plugin.jar \
           /usr/lib/jvm/default-jvm/jre/lib/ext/jfxrt.jar \
           /usr/lib/jvm/default-jvm/jre/bin/javaws \
           /usr/lib/jvm/default-jvm/jre/lib/javaws.jar \
           /usr/lib/jvm/default-jvm/jre/lib/desktop \
           /usr/lib/jvm/default-jvm/jre/plugin \
           /usr/lib/jvm/default-jvm/jre/lib/deploy* \
           /usr/lib/jvm/default-jvm/jre/lib/*javafx* \
           /usr/lib/jvm/default-jvm/jre/lib/*jfx* \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libdecora_sse.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libprism_*.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libfxplugins.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libglass.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libgstreamer-lite.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libjavafx*.so \
           /usr/lib/jvm/default-jvm/jre/lib/amd64/libjfx*.so

RUN curl -o /usr/local/bin/gosu -sSL "https://github.com/tianon/gosu/releases/download/1.2/gosu-amd64" && \
	chmod +x /usr/local/bin/gosu

RUN apk del wget ca-certificates && \
    rm /tmp/* /var/cache/apk/*

# Install Elasticsearch
RUN curl -Ls http://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$ES_VERSION/elasticsearch-$ES_VERSION.tar.gz | tar -xz -C /usr/share && \
    mv /usr/share/elasticsearch-$ES_VERSION /usr/share/elasticsearch
COPY ./elasticsearch.yml /usr/share/elasticsearch/elasticsearch.yml
COPY logging.yml /usr/share/elasticsearch/config/
COPY docker-entrypoint.sh /

ENV PATH /usr/share/elasticsearch/bin:$PATH

# Add elasticsearch user+group:
RUN addgroup -S elasticsearch && \
    adduser -S -G elasticsearch elasticsearch

RUN set -ex \
    && for path in \
       /usr/share/elasticsearch/data \
       /usr/share/elasticsearch/logs \
       /usr/share/elasticsearch/config \
       /usr/share/elasticsearch/config/scripts \
       ; do \
         mkdir -p "$path"; \
         chown -R elasticsearch:elasticsearch "$path"; \
       done

RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head && \
	/usr/share/elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf/2.0

VOLUME ["/usr/share/elasticsearch/data"]

EXPOSE 9200
EXPOSE 9300

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["elasticsearch", "-Des.network.host=0.0.0.0"]