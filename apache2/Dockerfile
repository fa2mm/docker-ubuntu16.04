FROM fa2m/ubuntu16.04

MAINTAINER fa2m

ARG web_path
ARG x_send_file_path
ARG internal_port

# install php and php-extensions
RUN apt -y install apache2 \
    libapache2-mod-xsendfile \
    && rm -rf /var/lib/apt/lists/*

# enable mod_rewrite
RUN a2enmod rewrite

# setup hosts file
ENV VHOST="<VirtualHost *:${internal_port}> \n\
    DocumentRoot \"${web_path}\" \n\
    XSendFile On \n\
    XSendFilePath \"${x_send_file_path}\" \n\
    <Directory \"/var/www/\"> \n\
        AllowOverride All \n\
        Require all granted \n\
    </Directory> \n\
</VirtualHost>"

RUN echo "${VHOST}" > /etc/apache2/sites-available/000-default.conf

RUN sed -i "s/^Listen [0-9]*/Listen ${internal_port}/g" /etc/apache2/ports.conf

RUN apt -y autoremove

RUN apt clean

EXPOSE ${internal_port}

ENTRYPOINT service apache2 start && /bin/bash

