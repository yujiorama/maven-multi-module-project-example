FROM docker.io/bellsoft/liberica-openjdk-alpine:11

RUN apk add --update tzdata \
 && ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
 && addgroup -g 1001 app \
 && adduser -h /app -H -G app -D -u 1001 app
