# This docker file will install mysql and our database
FROM postgres
RUN apt-get update -y
ENV POSTGRESQL_DATABASE main
ENV POSTGRESQL_ROOT_PASSWORD user

COPY ./sql-scripts/ /docker-entrypoint-initdb.d/