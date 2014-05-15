# Install PostgreSQL 9.3
FROM calamari/base

MAINTAINER Georg Tavonius "g.tavonius@gmail.com"


ENV PG_VERSION 9.3
ENV USER       docker
ENV PASS       SiHRDZ3Tt13uVVyH0ZST
ENV DB_NAME    docker


# Add the PostgreSQL PGP key to verify their Debian packages.
# It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# Add PostgreSQL's repository. It contains the most recent stable release of PostgreSQL 9.3.
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN apt-get -qq update

RUN apt-get -qqy install postgresql-$PG_VERSION postgresql-contrib-$PG_VERSION

# Run the rest of the commands as the ``postgres`` user created by the ``postgres-9.3`` package when it was ``apt-get installed``
USER postgres

# Create a PostgreSQL role named ``docker`` with ``docker`` as the password and
# then create a database `docker` owned by the ``docker`` role.
# Note: here we use ``&&\`` to run commands one after the other - the ``\``
#       allows the RUN command to span multiple lines.
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER $USER WITH SUPERUSER PASSWORD '$PASS';" &&\
    createdb -O $USER $DB_NAME

# ADD postgresql.conf etc/postgresql/$PG_VERSION/main/postgresql.conf
# ADD pg_hba.conf etc/postgresql/$PG_VERSION/main/pg_hba.conf
# ADD start_postgres.sh start_postgres.sh

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible.
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.3/main/pg_hba.conf

# And add ``listen_addresses`` to ``/etc/postgresql/9.3/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.3/main/postgresql.conf


EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# CMD ["sh", "/start_postgres.sh"]


# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/$PG_VERSION/bin/postgres", "-D", "/var/lib/postgresql/$PG_VERSION/main", "-c", "config_file=/etc/postgresql/$PG_VERSION/main/postgresql.conf"]
