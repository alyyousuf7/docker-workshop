# Images
OK, first of all, it's not `JPG` or `PNG` file that we're talking about here. It's important to learn a little about images because that's what will be used to run containers

Docker Images are just like `tar`/`zip` files. A Docker Image contains everything to setup a container.

We'll learn about how to create images in a later lesson, but for now, let's see what image name tells us.

## Tags
An image name is composed of two parts:

```
[image name]:[tag]
hello-world:latest
```

Tag is used to label an image with different version.

Suppose, I have an image that contains `v1.0` of my web server, I could tag it as `myserver:v1.0`.

Different tags can point to the same image. In the above case, the same image can also be tagged as `myserver:latest`, which will be pointing to the `myserver:v1.0` image.

In future, I can create another version of the image and tag it as `myserver:v2.0` and point `myserver:latest` to the newer image.

## Repository name
Repository name comes in when you pull an image uploaded by some user.

```
[repo name]/[image name]:[tag]
alyyousuf7/sshtron:latest
```

This represents that `alyyousuf7` is the owner of the image `sshtron:latest`.

You can pull the above image like this:

```bash
$ docker pull alyyousuf7/sshtron:latest
```

In case of, `hello-world:latest`, there is no repository name. That shows the image is owned/maintained by Docker Hub.

It is recommended that you use images that are maintained by Docker Hub. Some images maintained by them are listed below as examples:

- `hello-world:latest`
- `nginx:latest`
- `node:latest`
- `ubuntu:latest`

## Retagging Images
You can retag an image with a different name.

```bash
$ docker <old image name> <new image name>
```

Suppose, you wish to upload a copy of `hello-world:latest` image on your repository.

You'll first retag it.

```bash
$ docker tag hello-world:latest alyyousuf7/hello-world:latest
```

And then push it to the registry.

```bash
$ docker push alyyousuf7/hello-world:latest
```

It will give you an error that you're not logged in. You'll first need to create an account on [Docker Hub](https://hub.docker.com/) and login.

```bash
$ docker login
```

You're good to go!

Enough talking, let's play a little more with containers in the [next lesson](/lesson-5).
