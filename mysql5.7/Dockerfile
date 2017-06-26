FROM fa2m/ubuntu16.04

MAINTAINER fa2m

ARG mysql_root_pass
ARG mysql_db
ARG mysql_user
ARG mysql_user_pass

# install MySQL
RUN echo "mysql-server mysql-server/root_password password ${mysql_root_pass}" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password ${mysql_root_pass}" | debconf-set-selections
RUN apt -y install mysql-server

RUN service mysql start \
    && service mysql status \
    && { mysql -u root -p${mysql_root_pass} -e "CREATE DATABASE ${mysql_db}; \
            CREATE USER '${mysql_user}'@'%' IDENTIFIED BY '${mysql_pass}'; \
            GRANT ALL PRIVILEGES ON * . * TO '${mysql_user}'@'%' IDENTIFIED BY '${mysql_pass}' \
                WITH GRANT OPTION MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 \
                MAX_UPDATES_PER_HOUR 0 MAX_USER_CONNECTIONS 0; \
            GRANT ALL PRIVILEGES ON ${mysql_db} . * TO '${mysql_user}'@'%'"; }

# allow access from any ip (only DEV)
RUN sed -i 's/^bind-address.*127\.0\.0\.1/bind-address = 0\.0\.0\.0/g' /etc/mysql/mysql.conf.d/mysqld.cnf

RUN apt -y autoremove

RUN apt clean

EXPOSE 3306

ENTRYPOINT service mysql start && /bin/bash


