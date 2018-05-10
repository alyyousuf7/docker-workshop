# Install Docker
We'll use `curl` to install Docker:

```bash
$ curl -sSL get.docker.com | bash
```

Once installed, check if it is working properly:
```bash
$ sudo docker info
```

You have to use `sudo` for all Docker commands. It can become painful very quickly when you have to frequently enter Docker commands. To remedy this, we'll add your current user `$(whoami)`, to `docker` group:

```bash
$ usermod -aG docker $(whoami)
```

Once this is done, you will need to logout and login again to your computer so that the above change can take affect.

If you have logged in to a machine via SSH, just close the SSH session and login again.

To make sure that the user has been added to `docker` group, run the following command and expect no errors:

```bash
$ docker info
```

Voila, you just installed Docker! :tada:

Let's spin up a container in the [next lesson](/lesson-2).
