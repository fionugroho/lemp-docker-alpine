FROM alpine:3.14

LABEL Maintainer="Nugi" \
      Description="alpine nginx+php7fpm"

RUN apk update \
  && apk add --no-cache nginx supervisor php7 php7-fpm php7-mcrypt \
    php7-pdo_mysql \
    php7-gettext php7-xmlreader php7-xmlrpc \
    php7-bz2 php7-iconv php7-pdo_dblib php7-curl php7-ctype \
    php7-bcmath php7-gd php7-odbc \
    php7-soap php7-openssl php7-gmp \
    php7-pdo_odbc php7-json php7-dom \
    php7-pdo php7-zip php7-mysqli \
    php7-apcu php7-pdo_pgsql 

RUN apk --update add ca-certificates

COPY ../nugi/config/nginx/nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /etc/nginx/addconfig
COPY ../nugi/config/nginx/addconfig/* /etc/nginx
COPY ../nugi/config/nginx/sites-available /etc/nginx/
COPY ../nugi/config/nginx/sites-enable /etc/nginx/
COPY ../nugi/config/supervisord/supervisord.conf /etc/supervisord.conf

VOLUME ["/var/lib/nginx/html/"]
VOLUME ["/etc/nginx/"]
VOLUME [ "/etc/php7/" ]

RUN rm  -rf /tmp/* /var/cache/apk/*

EXPOSE 80
EXPOSE 443

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
