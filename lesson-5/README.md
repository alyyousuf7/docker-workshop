# Working inside a container
Container images provide you with minimal stuff, but you can always install new tools to work with.

Let's see if we can spin up a container and `curl https://aliyousuf.com`.

## Getting inside a container
```bash
$ docker run --interactive --tty ubuntu:latest
```

Here's some explanation:

- `--interactive` (or `-i`): attaches container's `stdin`, `stdout`
- `--tty` (or `-t`): attaches a psuedo-terminal with the current terminal

In short, it allows you interact with the container easily.

You might see something like this:

```bash
root@<container id>:/#
```

This represents that you're inside a container now.

## Let's do something
```bash
root@<container id>:/# ls
```

No problem, right? Let's `curl` now, it shouldn't be a problem.

```bash
root@<container id>:/# curl https://aliyousuf.com
bash: curl: command not found
root@<container id>:/#
```

What? But why did it fail?

Remember, I told you that Docker Images provides you with minimal tools. But you can install `curl` using `apt-get`.

```bash
root@<container id>:/# apt-get update && apt-get install curl -y
root@<container id>:/# curl https://aliyousuf.com
```

OK, since its working now, let's `curl` and save the data in a file and exit from the container because it's almost time to go home.

```bash
root@<container id>:/# mkdir mydata && cd mydata
root@<container id>:/mydata# curl https://aliyousuf.com > index.html
root@<container id>:/mydata# cat index.html
root@<container id>:/mydata# exit
```

Great, we downloaded a file, made sure it's there and exited from the container.

Let's make sure if the container is still there.

```bash
$ docker ps -a
```

Yup, its there but `EXITED`.

Also note the `COMMAND` column in `docker ps -a` output, `"/bin/bash"`. More about it later.

## Reuse `EXITED` container
If you run `docker run -it ubuntu:latest`, it will spin up another container with fresh data. This container will not have `/mydata/index.html` in it.

Kick start the older container so that you get your data back.

```bash
$ docker start <container id>
```

OK, but it didn't show anything? Because now it's running in the background, doing nothing. Let's get inside the container again by running `/bin/bash`.

```bash
$ docker exec -it <container id> /bin/bash
```

You have _executed_ a command manually inside a container and gain the access back. Make sure if your file is still there.

```bash
root@<container id>:/# cat mydata/index.html
root@<container id>:/# exit
```

The file is there. Good.

Note, if you do `docker ps` this time, it will show the container as `RUNNING`. That's something new.

This is because the command that you executed by `docker exec` is not the primary command that was used to run the container.

You might think that `/bin/bash` is exactly the same as primary command, but it's not the first one.

## Copy data from host to a container
Oh did you say you already have something on your host machine and you want it inside the container?

```bash
$ docker cp <src path> <container id>:<dst path>
```

Let's create a file and copy it to the container and see if it's there.

```bash
$ echo "hello world" > myfile.txt
$ docker cp myfile.txt <container id>:/mydata/hello-world.txt
$ docker exec -it <container id> cat /mydata/hello-world.txt
```

## Stop the container
You can stop the container now.

```bash
$ docker stop <container id>
```

It's back to `EXITED` state. Check it using `docker ps -a`.

## Save the changes
Use `docker commit`.

What? I have heard about `git commit`, what on Earth is `docker commit`?

Every command that you executed on a running container to install new tools or copied files to it, wouldn't it be nice to save them as a new image? Why not?

```bash
$ docker commit <container id> my-first-image:latest
```

Yes, it's that simple. Now you can run container from this image again and again.

```bash
$ docker run -it my-first-image:latest
```

Do you know what's simpler? [Dockerfiles](/lesson-6).
