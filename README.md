# Postges 9.4 server Docker container
It’s just regular Postgres database container that has one “patch” applied. The patch fixes the issue of new databases created with non UTF8 encoding.

If you encounter the following error when running Rails command `rake db:create` this Dockerfile can help you:
```
PGError: ERROR:  new encoding (UTF8) is incompatible with the encoding of the template database (SQL_ASCII)
HINT:  Use the same encoding as in the template database, or use template0 as template.
: CREATE DATABASE "System_test" ENCODING = 'unicode'
```

This Dockerfile applies the instructions given here: http://wiki.postgresql.org/wiki/Adventures_in_PostgreSQL%2C_Episode_1

## Build it
`[sudo] docker build -t postgresql .`

## Run it
```
docker run --restart="always" -d -P --name "container_name" --env 'DB_USER=username' --env 'DB_PASS=password' --env 'DB_NAME=dbname' image_name
```

## Example
```
docker run --restart="always" -d -P --name "postgres" --env 'DB_USER=giedrius' --env 'DB_PASS=giedrius' --env 'DB_NAME=giedrius_database' edvinasbartkus/postgres
```
