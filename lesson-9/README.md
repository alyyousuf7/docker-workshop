# Networks
When you deploy your application, you make sure that no unknown service can communicate with it.

For example, you have
- a UI for frontend
- an API server as backend
- a worker as helper to backend
- a database

Now you would not want anyone to access your worker and database directly. In some cases, you would not even want your API server to be exposed as well. So you put them on separate networks.

In Docker, you can create multiple networks and put your containers in one or more networks.

## Create network
Let's create some networks.

```bash
$ for net in $(echo frontend backend db); do \
    docker network create $net;              \
  done
```

The above command will create three different networks for you.

## List networks
You can check them up.

```bash
$ docker network ls
```

## Connect container to a network
Now we'll implement the following network:

```
    Internet
        |
  [reactjs-app] ---
        |         |--- frontend
  [nodejs-api]  ---
        |         |--- backend
     [worker]   ---
        |         |--- db
    [postgres]  ---
```

Let's do it.

```bash
# docker network connect [network] [container]
$ docker network connect frontend reactjs-app
$ docker network connect frontend nodejs-api
$ docker network connect backend  nodejs-api
$ docker network connect backend  worker
$ docker network connect db       worker
$ docker network connect db       postgres
```

This was simple! Guess what, we can make put it in a `docker-compose.yml`.

Find out what's `docker-compose.yml` in the [next lesson](/lesson-10).
