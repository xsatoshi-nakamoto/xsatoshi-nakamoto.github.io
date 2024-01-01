---
layout: post
title:  "Managing a docker images"
date:   2023-12-28 15:33:30 +0700
categories: Docker
---
# Managing Docker Images
We have already learned how to create Docker images. In this lesson, however, we will learn how to manage the images located
on a machine. We will demonstrate a few commands that are useful for downloading, inspecting, and removing images from the
system.
## Relevant Documentation
https://docs.docker.com/engine/reference/commandline/image/
## Lesson Reference
#### Download an image:

```
docker image pull nginx:1.14.0
```

#### List images on the system:

```
docker image ls
docker image ls -a
```

#### Inspect image metadata:

```
docker image inspect nginx:1.14.0
docker image inspect nginx:1.14.0 --format `"{{.Architecture}}"`
docker image inspect nginx:1.14.0 --format `"{{.Architecture}} {{.Os}}"`
```

####  Delete an image:

```
docker image rm nginx:1.14.0
```

#### Force deletion of an image that is in use by a container:

```
docker run -d --name nginx nginx:1.14.0
docker image rm -f nginx:1.14.0
```

#### Locate a dangling image and clean it up:

```
docker image ls -a
docker container ls
docker container rm -f nginx
docker image ls -a
docker image prune
```
