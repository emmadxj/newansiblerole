FROM mariadb
COPY . /var/cache/dockerbuild/mariadb
WORKDIR /var/cache/dockerbuild/mariadb

RUN ansible-playbook -i inventories/local.ini provisioning/install.yml -e '{ \
      "mariadb_dockerize_context" : "docker" }' && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN mkdir -p /etc/my_init.d && \
    cp scripts/startmariadb.sh /etc/my_init.d/10-mariadb && \
    chmod 0755 /etc/my_init.d/10-mariadb

VOLUME [ "/root", "/etc/mysql", \
         "/var/run/mysqld", "/var/lib/mysql", "/var/log/mysql" ]
# Expose ports.
EXPOSE 3306

