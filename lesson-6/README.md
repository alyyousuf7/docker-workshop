# Dockerfile
In the earlier lesson, we
- started a base container with `ubuntu:latest` image,
- installed a new tool, `curl`,
- hit a URL with `curl` and saved it's data in a file,
- copied a file from host to a container,
- finally, saved it as a new image.

Let's learn to do the same in a much more simpler, declarative way, using `Dockerfile`.

Before that, create a new directory on your host machine and work inside it. You'll find later why.

```bash
$ mkdir ~/docker-demo && cd ~/docker-demo # Create and move to a directory
$ echo "hello-world" > myfile.txt         # Create a file that we'll copy later
$ touch Dockerfile                        # Create an empty file where we'll do our work
```

Here's the `Dockerfile` for the stuff we did in previous lesson.

```Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install curl -y

WORKDIR /mydata

RUN curl https://aliyousuf.com > index.html

ADD myfile.txt hello.txt
```

Let's break it down.

## Line 1: `FROM <image name>`
Every Docker image has a base image. Or the image from which it spring off. Hence `FROM` is necessary in every `Dockerfile`.

Our image will be based on `ubuntu:latest` image.

## Line 2 & 4: `RUN <command>`
This is similar to `docker exec -it <command>`.

We're using it twice. Once to install `curl` and second to use `curl` to download a file.

## Line 3: `WORKDIR <path>`
`WORKDIR` changes the current working directory. If the directory doesn't exists, it creates the directory and `cd` into it.

Like in our case, we haven't created `/mydata` yet. But this command will create it for us.

You might wonder, why not use `RUN mkdir /mydata && cd /mydata`?

Every command (`RUN` or `ADD`, for example) uses the last value set by `WORKDIR` as the current working directory. So it saves you from adding `cd /mydata` to every other command.

## Line 5: `ADD <src path> <dst path>`
`ADD` performs the task of `docker cp` command. But in this case, we're using a relative paths, not absolute.

For `<dst path>`, you might have guessed it. Its absolute path becomes `<last workdir path>/<dst path>`.

For `<src path>`, it's a bit complicated. The absolute path it solves to is `<context path>/<src path>`.

But what is `<context path>`? Let's see it in the next heading.

## Building an image
Now you've got your `Dockerfile` ready, but how do you create an image using it?

```bash
$ docker build --file <path to Dockerfile> --tag <new image name> <context path>
```

So your command should look like this (with shorter flags):

```bash
$ docker build -f Dockerfile -t my-second-image:latest .
```

Yup, there's a period in the end. That's the context path, we've set it to use the current directory.

Context path is used by `Dockerfile` to resolve relative paths like in `ADD` command. That's how `ADD` command finds out where is the `myfile.txt` located.

Now, let's be more useful with our containers in the [next lesson](/lesson-7).
