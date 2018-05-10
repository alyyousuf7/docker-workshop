# Docker Compose
Just like `Dockerfile` makes creating images easier, Docker Compose makes deploying containers easier.

Docker Compose expects a YAML file, usually named `docker-compose.yml`, which contains information about what image to use to run containers, ports to expose, volumes to mount, networks, etc.

It let you run all of the above as single deployment, yet be scalable at the same time.

We'll not cover scalability in this workshop, but you can actually scale individual service independently. Read about [Docker Swarm](https://docs.docker.com/engine/swarm/) for more information.

## Installing Docker Compose
You have to download it separately, as it does not come with Docker.

```bash
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.1/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```

The above long command downloads and installs `docker-compose` to `/usr/local/bin`.

## Example Voting App
Docker has open-sourced a very good example of all the stuff we've learnt in the previous lessons and uses `docker-compose.yml` to deploy it.

https://github.com/dockersamples/example-voting-app

Read the [Architecture](https://github.com/dockersamples/example-voting-app#architecture) from the above repository description and come back.

Ready? Let's open up the `docker-compose.yml` file.

The file is pretty explainatory, but from a higher level, this is the format:

```yaml
version: "3"

services:
  [container 1 name]:
    [fixed image or build method]
    [ports to expose]
    [volumes to mount]
    [networks to mount]

  ...

volumes:
  [volume 1]:
    [mount mode and options]

  ...

networks:
  [network 1]:
    [mount mode and options]

  ...

...
```

Spin up the complete application.

```bash
$ docker-compose up
```

Now check all the running containers, or inspect each container for more details.

```bash
$ docker inspect <container id>
```

That's all folks!

Docker has many more features. Their documentation is very easy and the community is very strong.

You'll easily find help on the internet or join [Docker Community](https://www.docker.com/docker-community) on Slack for help.
