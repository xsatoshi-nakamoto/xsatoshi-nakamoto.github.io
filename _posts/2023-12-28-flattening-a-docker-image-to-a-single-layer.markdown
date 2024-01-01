---
layout: post
title:  "Flattening a Docker Image to a Single Layer."
date:   2023-12-28 15:33:30 +0700
categories: Docker
---
# Flattening a Docker Image to a Single Layer
In some rare cases, we may want to flatten the file system of a multi-layer image into a single layer. While Docker does not have
a simple command to do this, we can accomplish it by exporting a container's filesystem and importing it as an image. In this
lesson, we will see how to flatten an image filesystem into a single layer.
# Lesson Reference
#### Set up a new project directory to create a basic image:

```
cd ~/
mkdir alpine-hello
cd alpine-hello
vi Dockerfile
```

#### Create a Dockerfile that will result in a multi-layered image:

```
FROM alpine:3.9.3
RUN echo "Hello, World!" > message.txt
CMD cat message.txt
Build the image and check how many layers it has:
docker build -t nonflat .
docker image history nonflat
```

#### Run a container from the image and export its file system to an archive:

```
docker run -d --name flat_container nonflat
docker export flat_container > flat.tar
Import the archive to a new image and check how many layers the new image has:
cat flat.tar | docker import - flat:latest
docker image history flat
```
