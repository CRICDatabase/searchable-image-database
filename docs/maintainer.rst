Maintainer
==========

If you are the new maintainer,
this is for you.

GitHub
------

https://github.com/cricdatabase
is the organisation of the project on GitHub.
We store **all** our source code there.

Docker Hub
----------

https://hub.docker.com/orgs/cricdatabase
is the organisation of the project on Docker Hub.
We store Docker images there.

To build the image,
use ::

    $ docker build --target build-env -t repository/name:tagname .

To upload the image,
use ::

    $ docker push repository/name:tagname

Backend
^^^^^^^

Images for the backend in Node.js are available at
https://hub.docker.com/repository/docker/cricdatabase/nodejs.

Frontend
^^^^^^^^

Images for the backend in Angular are available at
https://hub.docker.com/repository/docker/cricdatabase/angular.
