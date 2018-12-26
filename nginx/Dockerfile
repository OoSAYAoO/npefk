FROM alpine:edge

ENV TIME_ZONE Asiz/Shanghai

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && apk upgrade && apk add --no-cache tzdata bash nginx && \
    echo "${TIME_ZONE}" > /etc/timezone && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime && \
    mkdir -p /run/nginx

EXPOSE 80

CMD /usr/sbin/nginx -g 'daemon off;'
