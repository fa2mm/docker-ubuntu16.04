FROM fa2m/ubuntu16.04

MAINTAINER fa2m

ARG mysql_root_pass
ARG mysql_db
ARG mysql_user
ARG mysql_user_pass

# install MySQL
RUN echo "mysql-server mysql-server/root_password password ''" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password ''" | debconf-set-selections
RUN sudo apt -y install mysql-server

RUN mysql -u root -p${mysql_root_pass} -e "CREATE DATABASE ${mysql_db}; CREATE USER '$mysql_user'@'%' IDENTIFIED BY '$mysql_pass'; GRANT ALL PRIVILEGES ON * . * TO '$mysql_user'@'%' IDENTIFIED BY '$mysql_pass' WITH GRANT OPTION MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 MAX_USER_CONNECTIONS 0; GRANT ALL PRIVILEGES ON `$mysql_db` . * TO 'sitesearch_us'@'%'";

# allow access from any ip (only DEV)
RUN sed -i 's/^bind-address.*127\.0\.0\.1/bind-address = 0\.0\.0\.0/g' /etc/mysql/mysql.conf.d/mysqld.cnf

# install apache2
RUN apt -y install apache2

# install php and php-extensions
RUN apt -y install php \
    libapache2-mod-php \
    php-mcrypt \
    php-mysql \
    php-xml \
    php-curl \
    php-mbstring \
    libapache2-mod-xsendfile \
    php-gd \
    php-bcmath \
    && rm -rf /var/lib/apt/lists/*

RUN service apache2 restart

RUN service mysql restart

RUN apt -y autoremove

RUN apt clean

# enable mod_rewrite
RUN a2enmod rewrite

EXPOSE 3306