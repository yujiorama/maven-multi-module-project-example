FROM debian:10-slim as builder

ARG MAJOR="11"
ARG MINOR="0"
ARG PATCH="10"
ARG REVISION="9"
ARG VERSION="${MAJOR}.${MINOR}.${PATCH}"
ARG TYPE="-lite"
ARG EXTRACT_DIR="jdk-${VERSION}${TYPE}"
ARG DOWNLOAD_URL="https://download.bell-sw.com/java/${VERSION}+${REVISION}/bellsoft-jdk${VERSION}+${REVISION}-linux-amd64${TYPE}.tar.gz"

ENV JAVA_HOME="/opt/jdk" \
    JAVA_OPTS="-Dfile.encoding=UTF-8 -Duser.timezone=Asia/Tokyo"

RUN set -x \
 && DEBIAN_FRONTEND=noninteractive apt-get update -q -y \
 && DEBIAN_FRONTEND=noninteractive apt-get install -q -y \
    ca-certificates \
    curl \
    gzip \
    tar \
    tzdata \
 && curl -fsSL "${DOWNLOAD_URL}" \
  | tar xzf - -C /opt \
 && mv "/opt/${EXTRACT_DIR}" "/opt/jdk" \
  ;

FROM gcr.io/distroless/base-debian10:latest

ARG MAJOR="11"
ARG MINOR="0"
ARG PATCH="10"
ARG REVISION="9"
ARG VERSION="${MAJOR}.${MINOR}.${PATCH}"

ENV JAVA_HOME="/opt/jdk" \
    JAVA_OPTS="-Dfile.encoding=UTF-8 -Duser.timezone=Asia/Tokyo"

COPY --from=builder "/opt/jdk" "/opt/jdk"
COPY --from=builder "/usr/share/zoneinfo/Japan" /etc/localtime
COPY --from=builder "/lib/x86_64-linux-gnu/libz.so.1" /lib/x86_64-linux-gnu/
