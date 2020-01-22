# Docker Compose Getting Started

This is built as a fork from [edm00se/simple-docker-compose-node-redis-demo](https://github.com/edm00se/simple-docker-compose-node-redis-demo), which is a [Node.js](https://nodejs.org/) re-interpretation of [the Docker "getting started" guide from their docs](https://docs.docker.com/compose/gettingstarted/). If you are unfamiliar with either, you should start there.

This project extends [edm00se/simple-docker-compose-node-redis-demo](https://github.com/edm00se/simple-docker-compose-node-redis-demo) by:

- adding [traefik](https://docs.traefik.io/) as a load balancer, via the `docker-compose.yml` config
- re-configuring the `Dockerfile` to expose the HTTP port, instead of solely within the `docker-compose.yml` configuration
  - this allows traefik to pick it up automagically
- the `app.js` response now incldues the container ID as "hostname" in the response

## Required

1. [Docker](https://www.docker.com/)
2. [Docker Compose](https://docs.docker.com/compose/install/) (this should come with [Docker CE / Docker Desktop](https://store.docker.com/search?offering=community&type=edition) for both macOS and Windows)

## Clone and Run

1. `git clone https://github.com/edm00se/proxy-simple-docker-compose-node-redis-demo.git`
2. `cd proxy-simple-docker-compose-node-redis-demo`
3. `docker-compose up` (first time run will perform build)
    - you can force a fresh build with `--build`
    - you can background (run without holding up your CLI) by using `--detach`
    - you can stop and remove the containers associated by substituting `down` in place of `up`
4. `docker-compose up -d --scale web=2` will scale up the "web" app service of our compose config to the specified number

## Test

```sh
curl -H Host:myapp.docker.localhost http://127.0.0.1
```

The "myapp" label is applied in the defined `labels:` field for the `docker-compose.yml` config definition of the web app "service". By specifying a `Host` header in our request, we are specifying a destination that traefik can interpret.

## License

The MIT License (MIT).
