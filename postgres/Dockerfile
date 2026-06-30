FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y postgresql-14 postgresql-contrib && \
    rm -rf /var/lib/apt/lists/*
USER postgres
RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER gitlab WITH PASSWORD 'gitlab_db_secret';" && \
    createdb -O gitlab gitlabhq_production
# CREATE USER建立使用者；ALTER USER修改使用者
# -O設定為擁有者 (Owner)
RUN echo "listen_addresses='*'" >> /etc/postgresql/14/main/postgresql.conf && \
    echo "host all all 0.0.0.0/0 md5" >> /etc/postgresql/14/main/pg_hba.conf
EXPOSE 5432
VOLUME ["/var/lib/postgresql/14/main"]
CMD ["/usr/lib/postgresql/14/bin/postgres", "-D","/var/lib/postgresql/14/main", "-c","config_file=/etc/postgresql/14/main/postgresql.conf"]
