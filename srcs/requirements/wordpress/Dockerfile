FROM	alpine:3.14

RUN		apk update --quiet
RUN		apk add --quiet --no-cache --update curl bash
RUN		apk add --quiet --no-cache --update mariadb-client
RUN		apk add --quiet --no-cache --update php7 php-phar \
			php-json php-curl php-fpm php-mysqli php-iconv

RUN		mkdir -p /var/www/wordpress 

RUN		curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
			--output /usr/bin/wp 

RUN		chmod +x ./usr/bin/wp 

RUN		wp core download --path=/var/www/wordpress

WORKDIR /var/www/wordpress

COPY	config/wp-config /config/wp-config

COPY	./scripts/entrypoint.sh /tmp/entrypoint.sh

RUN		chmod +x /tmp/entrypoint.sh

ENTRYPOINT ["sh", "/tmp/entrypoint.sh"]