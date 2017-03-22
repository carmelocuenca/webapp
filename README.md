# Aplicación básica en Rails 5

A Rails 5 application with PostgreSQL with 1 table to "trastear " with Docker.

```
$ git clone bla bla bla
```

To buid the Docker iamge

```
$ cd webapp
$ docker build -t webapp .
```

To start postgresql server

```
$ docker run --name some-postgres \
  -e POSTGRES_USER=${POSTGRES_USER}
  -e POSTGRES_PASSWORD=${POSTGRES_PASSWORD} -d postgres
```

To setup and migrate
```
$ docker run  --link some-postgres:db \
  -e "POSTGRES_USER=${POSTGRES_USER}" \
  -e "POSTGRES_PASSWORD=${POSTGRES_PASSWORD}" \
  -v "$PWD":/usr/src/app -w /usr/src/app webapp  bin/rails db:setup
...
$ docker run  --link some-postgres:db \
  -e "POSTGRES_USER=${POSTGRES_USER}" \
  -e "POSTGRES_PASSWORD=${POSTGRES_PASSWORD}" \
  -v "$PWD":/usr/src/app -w /usr/src/app webapp  bin/rails db:migrate

```

To run the image
```
$ docker run  --rm -it --link some-postgres:db \
  -e "POSTGRES_USER=${POSTGRES_USER}" \
  -e "POSTGRES_PASSWORD=${POSTGRES_PASSWORD}" \
  -v "$PWD":/usr/src/app -w /usr/src/app -p 8080:3000 webapp
```
