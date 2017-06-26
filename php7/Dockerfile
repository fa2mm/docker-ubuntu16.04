FROM fa2m/ubuntu16.04

MAINTAINER fa2m

# install php and php-extensions
RUN apt -y install php \
    php-mcrypt \
    php-xml \
    php-curl \
    php-mbstring \
    php-gd \
    php-bcmath \
    && rm -rf /var/lib/apt/lists/*

