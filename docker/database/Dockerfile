FROM mariadb:12.0.2

VOLUME /var/lib/mysql
EXPOSE 3306

RUN touch /var/log/mysql.log
RUN chown mysql:mysql /var/log/mysql.log
COPY ./docker/database/myconf.cnf /etc/mysql/conf.d/.