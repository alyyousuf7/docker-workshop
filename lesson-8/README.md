# Use containers to compile tools
So, your friend made a tool that you really like. He made it using a language you're not familiar with.

But you don't want to download and install all the dependencies it requires to compile.

For the sake of a realy example, let's pick a game I created a few days ago using Golang. It's 2048 game playable on command-line. Sounds fun, eh?

>https://github.com/alyyousuf7/twenty48

Let's clone the repository and have a look at it's `Dockerfile`.

```bash
$ git clone https://github.com/alyyousuf7/twenty48.git
$ cd twenty48 && cat Dockerfile
```

Pretty small file, right? There's more to it.

I have made a `Makefile` which lets you,
- get inside a container pretty quickly using `make shell`
- and compile the Golang binary using `make binary`

```bash
$ make shell
root@<container id>:/go/src/github.com/alyyousuf7/twenty48# make binary
root@<container id>:/go/src/github.com/alyyousuf7/twenty48# exit
$ ./bin/twenty48
```

You just compiled your first Golang program without even install Golang on your machine! Isn't this cool?

## Explanation
When you ran `make shell`, it executed the following Docker commands:

```bash
$ docker build -t twenty48:latest .
$ docker run -v $(pwd)/bin:/go/src/github.com/alyyousuf7/twenty48/bin twenty48:latest
```

It created a Docker image and ran it's container with a directory mounted to your host machine.

When you ran `make binary` inside the container, it ran the `go build` command and output the binary in `bin` directory inside the container.

Since the `bin` directory was mounted, the `twenty48` binary was copied to your host machine as well.

In the [next lesson](/lesson-9), we'll learn how to connect multiple containers and communicate in private.
