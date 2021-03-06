FROM php:7.1.7-apache

RUN apt-get update && apt-get install -y --no-install-recommends \
        curl \        
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libssl-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        libxml2-dev \
        php-soap \
        zlib1g-dev \
        libicu-dev \
        g++ \
        git

## Install mcrypt and gd
RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

## Install Mysql and mysql PDO
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql 

## Install Postgres 
RUN docker-php-ext-install pdo_pgsql

## Install Soap
RUN docker-php-ext-install soap 

## Install XDEBUG
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug 

## Install Mongodb
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb 

## Install ZIP
RUN docker-php-ext-install zip 

## Install BCMATH
RUN docker-php-ext-install bcmath 

## Install Exif
RUN docker-php-ext-install exif 

## Install TOKENIZER
RUN docker-php-ext-install tokenizer 

## Install Human Language and Character Encodeing Support

RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl 

## Install Redis
RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis 

## Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

## Install NodeJS and NVM
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt install nodejs \
    && apt install build-essential 

## Install Gulp
RUN npm install -g gulp

## Install wkhtml
RUN apt install xvfb libfontconfig wkhtmltopdf -y

RUN a2enmod rewrite

RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www

WORKDIR /var/www/html

EXPOSE 80