This repository contains code underpinning the database used by the Center for Recognition and Inspection of Cells (CRIC) at Universidade Federal de Ouro Preto in Brazil. 

# Center for Recognition and Inspection of Cells (CRIC) 

[CRIC Searchable Image Database](https://cricdatabase.com.br/) is a public database containing cervical cell images. This database helps analyse results of commonly
used Pap smear for any signs of cervical cancer. The database was created and is maintained at the 
All data in the database has been anonymised.
The database has been using the code in this repository since 01 July, 2020.

# Develop

In order to run the database locally you need to have [Docker](https://docs.docker.com/install/) installed. 

## Setup

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
$ docker-compose exec nodejs npx sequelize db:create
$ docker-compose exec nodejs npx sequelize db:migrate
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

- `nodejs`
- `db`
- `angular`
