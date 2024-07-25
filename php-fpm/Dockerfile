FROM php:7.2-fpm

COPY ./sources.list /etc/apt/sources.list

WORKDIR "/server"

RUN echo "date.timezone = Europe/Paris" > /usr/local/etc/php/conf.d/timezone.ini

# Install selected extensions and other stuff
RUN docker-php-ext-install pdo pdo_mysql bcmath
RUN sed -i "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" /usr/local/etc/php-fpm.d/www.conf

RUN echo "override"
COPY php-ini-overrides.ini /usr/local/etc/php/conf.d/99-overrides.ini

# Install sudo
RUN apt-get update \
    && apt-get -y install sudo \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install zip
RUN apt-get update \
    && apt-get -y install zip unzip \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install openssl
RUN apt-get update \
    && apt-get -y install openssl \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install supervisor
RUN apt-get update \
    && apt-get -y install supervisor \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

# create user
RUN groupadd smm
RUN useradd -r -u 1000 -g smm smm
RUN usermod -a -G sudo smm
RUN mkdir /home/smm
RUN chown -R smm:smm /home
RUN echo "dev\ndev" | passwd

CMD sleep 10 && supervisord && supervisorctl start all && php-fpm
