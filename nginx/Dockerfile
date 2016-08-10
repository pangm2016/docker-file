FROM ubuntu:14.04

MAINTAINER pangm "pangm@asto-inc.com"

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY nginx_signing.key /root/nginx_signing.key
COPY sources.list /etc/apt/sources.list

RUN apt-key add /root/nginx_signing.key \
    && apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
    ca-certificates  nginx-module-xslt nginx-module-geoip nginx-module-image-filter nginx-module-perl nginx-module-njs gettext-base \
    && apt-get install curl telnet -y && rm -rf /var/lib/apt/lists/* 

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
