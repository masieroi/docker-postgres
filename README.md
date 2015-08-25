# Docker image for Postgres 
Originally forked from https://github.com/macadmins/postgres

The image is build in docker registry: https://hub.docker.com/r/masieroi/postgres/

Docker container for PostgreSQL that accepts remote connections from all addresses so it is intended to be be used on a local development environment 

The image is designed to be used with [Liferay Docker container](https://hub.docker.com/r/masieroi/liferay/).

In addition, we can automaticazlly add a new user/database according to the following environment variables:  
DB_NAME database  
DB_USER admin  
DB_PASS password  

To start the container
```
docker run -p 5432:5432 -e DB_NAME=lportal -e DB_USER=lportal -e DB_PASS=lportal -d --name protones-postgres --volumes-from liferay-postgres-data masieroi/postgres:9.3.5
```

If you want to isolate the data folder you can use a light Busybox image https://hub.docker.com/_/busybox/

```
docker create -v /var/lib/postgresql/data --name liferay-postgres-data busybox
```

then start the Postgres container linking the data folder to the Busybox *liferay-postgres-data*

```
docker run -p 5432:5432 -e DB_NAME=lportal -e DB_USER=lportal -e DB_PASS=lportal -d --name protones-postgres --volumes-from liferay-postgres-data masieroi/postgres:9.3.5
```
