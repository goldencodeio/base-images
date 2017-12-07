FROM bitrixdock/php71-fpm:latest
LABEL maintainer="Constantine Karnaukhov <genteelknight@gmail.com>"

RUN usermod -u 1000 www-data

# INSTALL NGINX
RUN apt-get update \
	&& apt-get install -y nginx \
	&& apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# PHP CONFIGS
ADD ./php.ini /etc/php/7.1/fpm/conf.d/90-php.ini
ADD ./php.ini /etc/php/7.1/cli/conf.d/90-php.ini

# NGINX CONFIGS
ADD conf/nginx.conf /etc/nginx/
ADD conf/default.conf /etc/nginx/sites-available/default
ADD conf/upstream.conf /etc/nginx/conf.d/
ADD www/index.html /var/www/html/

WORKDIR "/var/www/bitrix"

ADD ./run.sh /
RUN chmod +x /run.sh
CMD ["/run.sh"]

EXPOSE 80 443
