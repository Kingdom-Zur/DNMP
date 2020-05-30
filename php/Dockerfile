#基础镜像
FROM php:fpm
#添加一些依赖
#COPY ./root/ /
#安装自带但默认未开启的扩展
RUN docker-php-ext-install pdo_mysql
#安装redis扩展
RUN apt update && apt install -y libssl-dev \
    && curl -o swoole.tar.gz -fsSL 'https://github.com/swoole/swoole-src/archive/master.tar.gz' \
    && mkdir -p /tmp/swoole \
    && tar -xf swoole.tar.gz -C /tmp/swoole --strip-components 1 \
    && rm swoole.tar.gz \
    && docker-php-ext-configure /tmp/swoole --with-openssl-dir=/usr/include/openssl --enable-openssl --enable-http2 \
    && docker-php-ext-install /tmp/swoole \
    && rm -r /tmp/swoole \
    && curl -fsSL 'https://github.com/phpredis/phpredis/archive/5.2.1-liveness.tar.gz' -o redis.tar.gz \
    && mkdir -p /tmp/redis \
    && tar -xf redis.tar.gz -C /tmp/redis --strip-components=1 \
    && rm redis.tar.gz \
    && docker-php-ext-configure /tmp/redis --enable-redis \
    && docker-php-ext-install /tmp/redis \
    && rm -r /tmp/redis
