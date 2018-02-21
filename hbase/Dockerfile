# Dockerfile for HBase
FROM alpine:latest
LABEL Maintainer="James J. Attard <info@jamesattard.com>"
ARG HBASE_VERSION=1.3.1
LABEL Description="HBase $HBASE_VERSION"

ENV PATH $PATH:/hbase/bin
ENV JAVA_HOME=/usr
ENV URL=http://www.apache.org/dyn/closer.lua?filename=hbase/$HBASE_VERSION/hbase-$HBASE_VERSION-bin.tar.gz&action=download \
  URL_ARCHIVE=http://archive.apache.org/dist/hbase/$HBASE_VERSION/hbase-$HBASE_VERSION-bin.tar.gz

WORKDIR /

RUN set -euxo pipefail \
  && apk add --no-cache bash openjdk8-jre-base wget tar

RUN set -euxo pipefail \
  && wget -t 10 --max-redirect 1 --retry-connrefused -O "hbase-$HBASE_VERSION-bin.tar.gz" "${URL}" \
  || wget -t 10 --max-redirect 1 --retry-connrefused -O "hbase-$HBASE_VERSION-bin.tar.gz" "${URL_ARCHIVE}" \
  && mkdir "hbase-$HBASE_VERSION" \
  && tar zxf "hbase-$HBASE_VERSION-bin.tar.gz" -C "hbase-$HBASE_VERSION" --strip 1 \
  && test -d "hbase-$HBASE_VERSION" \
  && ln -sv "hbase-$HBASE_VERSION" hbase \
  && rm -fv "hbase-$HBASE_VERSION-bin.tar.gz" \
  && { rm -rf hbase/{docs,src}; : ; } \
  && apk del tar wget

ADD entrypoint.sh /
ADD conf/hbase-site.xml /hbase/conf/
ADD profile.d/java.sh /etc/profile.d/

# Stargate  8080  / 8085
# Thrift    9090  / 9095
# HMaster   16000 / 16010
# RS        16201 / 16301
EXPOSE 2181 8080 8085 9090 9095 16000 16010 16201 16301

CMD "/entrypoint.sh"