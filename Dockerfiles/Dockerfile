# Fetch php-apache image from dockerhub
FROM php:7.4-apache

WORKDIR /app

# Installing dependencies
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    wget \
    libicu-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
	&& docker-php-ext-install mysqli
	
# Setting up mediawiki build to apache root
RUN wget https://releases.wikimedia.org/mediawiki/1.41/mediawiki-1.41.1.tar.gz
RUN tar xvzf mediawiki-1.41.1.tar.gz
RUN mv mediawiki-1.41.1 /var/www/html/mediawiki
RUN rm -rf mediawiki-1.41.1.tar.gz

