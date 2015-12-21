# Fabio Docker Compose

fabio is a fast, modern, zero-conf load balancing HTTP(S) router for deploying microservices managed by consul.
See https://github.com/eBay/fabio

# Boot the infrastructure

We assume that you have installed the Docker Toolbox.

You can start consul, registrator and fabio with docker compose:
> docker-compose up -d

Consul UI:
> http://192.168.99.100:8500/

# Demo

Let's start a hello world container:
> docker run -d --name hello-world-1 -p 80 -e SERVICE_TAGS=urlprefix-/ -e SERVICE_CHECK_HTTP=/ tutum/hello-world

Find out wich port this container is running with:
> docker ps | grep hello-world

Access the hello world page using this port:
> curl http://192.168.99.100:32771

Access the hellow world page using fabio:
> curl http://192.168.99.100:9999/

We can start more hello-world containers like:
> docker run -d --name hello-world-2 -p 80 -e SERVICE_TAGS=urlprefix-/ -e SERVICE_CHECK_HTTP=/ tutum/hello-world

> docker run -d --name hello-world-3 -p 80 -e SERVICE_TAGS=urlprefix-/ -e SERVICE_CHECK_HTTP=/ tutum/hello-world

Access the hellow world page using fabio (e.g. round robin will be used):
> curl http://192.168.99.100:9999/

# Magement Interface

Fabio Management Interface:
> http://192.168.99.100:9998/