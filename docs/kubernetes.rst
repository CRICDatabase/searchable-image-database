Kubernetes
==========

..  note::

    You can use ``kubectl apply``
    to update resources.

..  note::

    To have https://cricdatabase.com.br/ directing users
    to the new Kubernetes cluster,
    you will have to update the DNS.

Docker to Kubernetes
--------------------

Kubernetes configuration files are generated from ``docker-compose.yml``::

    $ kompose convert -f docker-compose.yml -o k8s

DigitalOcean
------------

Visit https://cloud.digitalocean.com/kubernetes
and create a new cluster.
More information at https://www.digitalocean.com/docs/kubernetes/quickstart/.

..  note::

    DigitalOcean floating IPs are publicly-accessible static IP addresses.
    You need to create one and assign to the Kubernetes cluster.
    More information at https://www.digitalocean.com/docs/networking/floating-ips/quickstart/.

Download the configuration file
and load it to your Kubernetes configuration file.

Check the current default context::

    $ kubectl config current-context

Create a namespace called ``cricdatabase``::

    $ kubectl create namespace cricdatabase

Now, list all the namespaces in your cluster::

    $ kubectl get namespace

Deploy the Block Storage Volume pods into the ``cricdatabase`` namespace::

    $ kubectl apply -f k8s/db-data.yaml -n cricdatabase
    $ kubectl apply -f k8s/nodejs-image.yaml -n cricdatabase
    $ kubectl apply -f k8s/angular-log-data.yaml -n cricdatabase

Check the pod is up and running in the cluster::

    $ kubectl get pvc -n cricdatabase

Deploy the ConfigMap into the ``cricdatabase`` namespace::

    $ kubectl apply -f k8s/mysql-dev-env-configmap.yaml -n cricdatabase
    $ kubectl apply -f k8s/mysql-prod-env-configmap.yaml -n cricdatabase

Check the ConfigMap is up and running in the cluster ::

    $ kubectl get configmap -n cricdatabase

Deploy the (Deployment) pods into the ``cricdatabase`` namespace::

    $ kubectl apply -f k8s/db-deployment.yaml -n cricdatabase
    $ kubectl apply -f k8s/nodejs-deployment.yaml -n cricdatabase
    $ kubectl apply -f k8s/angular-deployment.yaml -n cricdatabase

Check the pod is up and running in the cluster::

    $ kubectl get pod -n cricdatabase

If one of your pods has status ``CrashLoopBackOff``,
get more information using::

    $ kubectl describe pod chashed-pod-name -n cricdatabase

If you need to access the log,
use ::

    $ kubectl logs pod-name -n cricdatabase

..  note::

    For crashed pods,
    you want to look at the previous pod::

        $ kubectl logs -p pod-name -n cricdatabase

You can also connect to the log sreaming using the ``-f`` flag ::

    $ kubectl logs -f pod-name -n cricdatabase

To gain Shell access to the pod::

    $ kubectl exec -n cricdatabase -i -t pod-name -- /bin/bash

..  important::

    You **need** to access the nodejs pod to create the database
    and tables.
    Also,
    you need to create the directories to store the imaages.

If the pods are up and running,
you need to include then in the network ::

    $ kubectl apply -f k8s/db-service.yaml -n cricdatabase
    $ kubectl apply -f k8s/nodejs-service.yaml -n cricdatabase
    $ kubectl apply -f k8s/angular-service.yaml -n cricdatabase

Check that the services are working ::

    $ kubectl get service -n cricdatabase

We need to forward a local port to the pod
to access the running app locally::

    $ kubectl port-forward pods/angular -n cricdatabase 8080:4200
    $ kubectl port-forward pods/nodejs -n cricdatabase 3000:3000

Open http://localhost:8080 with your web browser
and you should see the website.

If the website is working as expected,
is time to open it to the world ::

    $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml
    $ kubectl apply -f k8s/cricdatabase-configmap.yaml -n ingress-nginx

Create a DigitalOcean Load Balancer
that will load balance
and
route HTTP and HTTPS traffic to the Ingress Controller Pod
deployed in the previous command ::

    $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/provider/cloud-generic.yaml

DigitalOcean will provide you with an external IP address
that you can use to access the Nginx Ingress
which will direct the traffic to you application. ::

    $ kubectl get service ingress-nginx -namespace ingress-nginx

The rules of how Nginx Ingress will direct the traffic
need to be provided ::

    $ kubectl apply -f k8s/cricdatabase-ingress.yaml -n cricdatabase

To test if things are working,
you can use ``curl`` to resolve the DNS
to the IP address that DigitalOcean is providing.
::

  $ curl --resolve "cricdatabase.com.br:80:xxx.xxx.xxx.xxx" http://cricdatabase.com.br/api 
  $ curl --resolve "cricdatabase.com.br:80:xxx.xxx.xxx.xxx" http://cricdatabase.com.br

When you’re done,
delete the services ::

    $ kubectl delete service db -n cricdatabase
    $ kubectl delete service nodejs -n cricdatabase
    $ kubectl delete service angular -n cricdatabase

delete the pods ::

    $ kubectl delete deployment db -n cricdatabase
    $ kubectl delete deployment nodejs -n cricdatabase
    $ kubectl delete deployment angular -n cricdatabase

delete the ConfigMap ::

    $ kubectl delete configmap mysql-dev-env -n cricdatabase
    $ kubectl delete configmap mysql-prod-env -n cricdatabase

delete the Persistent Volume Claim ::

    $ kubectl delete pvc node-image -n cricdatabase
    $ kubectl delete pvc db-data -n cricdatabase

delete the Persistent Volume ::

    $ kubectl delete pv node-image
    $ kubectl delete pv db-data

And the Kubernetes cluster.
