Docker
======

`Docker <https://www.docker.com/>`_ uses OS-level virtualization to deliver software in packages called containers.

Requirements
------------

You need to have Docker installed.
Instructions are available at https://docs.docker.com/install/.

Submodules
----------

You will need

- https://github.com/CRICDatabase/searchable-image-database-nodejs/
- https://github.com/CRICDatabase/searchable-image-database-angular/

If you cloned the project using ::

    $ git clone --recurse-submodules git@github.com:CRICDatabase/searchable-image-database.git

you already have the submodules.

If you don't have the submodules,
run ::

    $ git submodule init
    $ git submodule update

Running
-------

To create the containers (if need)
and launch them,
execute ::

    $ docker-compose up --abort-on-container-exit

The first time,
``docker-compose`` will download some images.
This process will take some time but will **only** happen during the first time.
Also,
you need to create the database by running ::

    $ docker-compose exec nodejs npx sequelize db:create
    $ docker-compose exec nodejs npx sequelize db:migrate

Access http://localhost:8080/ from your web browser
to test the CRIC Searchable Image Database.

To stop the containers,
execute ::

    $ docker-compose stop

If you need to inspect any of the containers,
use ::

    $ docker-compose exec SERVICE sh

where ``SERVICE`` is one of the services defined at ``docker-compose.yml``:

- ``nodejs``
- ``db``
- ``angular``

Load Real Data
--------------

If you have access to the SQL dump,
you can load it into container cluster::

    $ docker-compose exec -T db mysql -p123.456 cric < nodejs.sql
