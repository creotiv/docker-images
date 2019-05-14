FROM ubuntu:18.04

LABEL maintainer="creotiv" email="creotiv@gmail.com"

ARG NGINX_VERSION=1.12.2
ARG JANSSON_VERSION=2.10
ENV LD_LIBRARY_PATH=/usr/local/lib

WORKDIR /root/dl

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-upgrade --no-install-suggests unzip gcc zlib1g-dev libssl-dev wget  libxml2-dev libxslt-dev libjansson-dev libjwt-dev && \
    wget --no-check-certificate https://github.com/TeslaGov/ngx-http-auth-jwt-module/archive/master.zip && \
    unzip master.zip && \
    rm master.zip && \
    wget http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz && \
    tar -xzf nginx-$NGINX_VERSION.tar.gz && \
    rm nginx-$NGINX_VERSION.tar.gz && \
    ln -sf nginx-$NGINX_VERSION nginx && \
    cd /root/dl/nginx && \
    mkdir -p /usr/lib64/nginx/modules/ && \
    ./configure \
      --add-dynamic-module=../ngx-http-auth-jwt-module-master \
      --prefix=/usr/share/nginx \
      --sbin-path=/usr/sbin/nginx \
      --modules-path=/usr/lib64/nginx/modules \
      --conf-path=/etc/nginx/nginx.conf \
      --error-log-path=/var/log/nginx/error.log \
      --http-log-path=/var/log/nginx/access.log \
      --pid-path=/run/nginx.pid \
      --lock-path=/run/lock/subsys/nginx \
      --user=root \
      --group=root \
      --with-file-aio \
      --with-ipv6 \
      --with-http_ssl_module \
      --with-http_v2_module \
      --with-http_gunzip_module \
      --with-http_gzip_static_module \
      --with-http_random_index_module \
      --with-http_degradation_module \
      --with-http_slice_module \
      --with-http_stub_status_module \
      --with-stream=dynamic \
      --with-stream_ssl_module && \
    make && make install && make modules && \
    cp /root/dl/nginx/objs/ngx_http_auth_jwt_module.so /usr/lib64/nginx/modules/ && \
    apt-get -y purge unzip wget gcc libxml2-dev libxslt-dev zlib1g-dev && \
    apt-get autoremove -y

COPY resources/nginx.conf /etc/nginx/nginx.conf
COPY resources/jwt-nginx.conf /etc/nginx/conf.d/jwt-nginx.conf

CMD ["nginx"]
