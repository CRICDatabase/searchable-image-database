# CRIC Searchable Image Database

CRIC Searchable Image Database is a public cervical cell image database aiming supporting cervical cancer analysis of Pap smear.

https://cricdatabase.com.br/ used this source code from 01 July, 2020.

## Submodules

- https://github.com/CRICDatabase/searchable-image-database-nodejs/
- https://github.com/CRICDatabase/searchable-image-database-angular/

## Testing (with Docker)

To create the containers (if need)
and launch them,
execute

```
$ docker-compose up --abort-on-container-exit
```

The first time,
`docker-compose` will download some images.
This process will take some time but will **only** happen during the first time.
Also,
you need to create the database by running

```
$ docker-compose exec node npx sequelize db:create
$ docker-compose exec node npx sequelize db:migrate
```

Access [http://localhost:8080/](http://localhost:8080/) from your web browser
to test the CRIC Searchable Image Database.

To stop the containers,
execute

```
$ docker-compose stop
```

If you need to inspect any of the containers,
use

```
$ docker-compose exec SERVICE sh
```

where `SERVICE` is one of the services defined at `docker-compose.yml`:

- `node`
- `db`
- `angular`
