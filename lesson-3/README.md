# Registry
Registry is a place where you can upload and reuse the images uploaded by other users.

[Docker Hub](https://hub.docker.com/) is a registry maintained by Docker itself. You can upload your own images, or find all the official images from there, even the `hello-world:latest` image that we used earlier.

Docker has a command to search for images through CLI, for example:
```bash
docker search nginx
```

## Pull an image
In the earlier lesson when we ran, `docker run hello-world:latest`, it pulled the image itself. But it is possible to pull an image beforehand to save time:
```bash
docker pull <image name>
```

It will take some time to pull, depending on the size of the image.

## List the images
Let's see where does it show up after its pulled:

```bash
$ docker image ls
```

The list will show you all the images, with their tags and the time when they were updated.

## Remove an image
Sometimes you've pulled so many images that your disk run out of space. So you should remove all the unwanted images:

```bash
$ docker rmi <image name>
```

`rmi` stands for `remove image`.

Let's talk a little more about images in the [next lesson](/lesson-4).
