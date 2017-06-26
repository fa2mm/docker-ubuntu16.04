FROM fa2m/ubuntu16.04

MAINTAINER fa2m

ARG mysql_root_pass

# install php and php-extensions
RUN apt -y install apache2 \
    && rm -rf /var/lib/apt/lists/*

# enable mod_rewrite
RUN a2enmod rewrite

# setup hosts file
RUN VHOST=$(cat <<EOF
<VirtualHost *:80>
    DocumentRoot "/var/www/sitesearch/app/web/"
    XSendFile On
    XSendFilePath /var/www/sitesearch/app/data/
    <Directory "/var/www/">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
EOF
) && echo "${VHOST}" > /etc/apache2/sites-available/000-default.conf

RUN apt -y autoremove

RUN apt clean

EXPOSE 80

ENTRYPOINT service mysql start && /bin/bash

