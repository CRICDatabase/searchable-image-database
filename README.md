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

Access [http://localhost:9229/](http://localhost:9229/) from your web browser
to test the CRIC Searchable Image Database.

To stop the containers,
execute

```
$ docker-compose stop
```

If you need to inspect any of the containers,
use

```
$ docker-compose exec CONTAINER sh
```

where `CONTAINER` is `node` or `sangular`.
