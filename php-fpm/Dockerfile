FROM alpine:edge

ENV TIME_ZONE Asiz/Shanghai
ENV PHP_MEMORY_LIMIT 128M
ENV MAX_UPLOAD 20M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST 20M

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && apk upgrade && apk add --no-cache tzdata curl tar xz libressl bash && \
    echo "${TIME_ZONE}" > /etc/timezone && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime && \
    apk add --no-cache autoconf dpkg-dev dpkg file g++ gcc libc-dev make pkgconf re2c argon2-dev \
        curl-dev libedit-dev libsodium-dev libxml2-dev sqlite-dev

RUN apk add --repository http://mirrors.ustc.edu.cn/alpine/edge/testing/ --no-cache php7 php7-apcu \
        php7-bcmath php7-ctype php7-curl php7-fpm php7-gd php7-iconv php7-intl \
        php7-json php7-ldap php7-sodium php7-mbstring php7-mcrypt php7-memcached php7-mongodb php7-msgpack \
        php7-mysqli php7-mysqlnd php7-opcache php7-openssl php7-pdo php7-pdo_mysql php7-posix php7-redis \
        php7-simplexml php7-soap php7-xml php7-xmlrpc php7-zip

RUN sed -i "s|;*daemonize\s*=\s*yes|daemonize = no|g" /etc/php7/php-fpm.conf && \
    sed -i "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*listen\s*=\s*/||g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php7/php.ini && \
    mkdir /www

EXPOSE 9000

CMD /usr/sbin/php-fpm7 --nodaemonize
