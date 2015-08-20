## What is Docker?
Docker is an open platform for building, shipping and running distributed applications. It gives programmers, development teams and operations engineers the common toolbox they need to take advantage of the distributed and networked nature of modern applications. [Read more about Docker](https://www.docker.com/)

## Preparations
I use docker daily basis for the projects, so I don't have to install it. But if I would have to start from scratch I would read thoroughly the [linux installation guide](http://docs.docker.com/linux/step_one/), since my workstation runs [XUbuntu](http://xubuntu.org/tour/).

## Some of the most used commands, which gathered since we started using docker
* build image from Dockerfile
```bash
$ docker build
```
* create a new instance of docker image and run it
```bash
$ docker run
```
* suspend / continue the running of an image 
```bash
$ docker start
$ docker stop
```
* show images
```bash
$ docker images
```
* show running / all containers 
```bash
$ docker ps
$ docker ps -a
```
* remove all docker images 
```bash
$ docker rmi $(docker images -q)
```
* remove all docker containers
```bash
$ docker rm $(docker ps -a -q)
```
* run a command (eg. bash) in a container 
```bash
$ docker exec -it [container-id or container-name] /bin/bash
```

## Enough talking do some actual code!
### Phase1 - set up a container with nodejs

* Google always has great stuff for the developers, this time I will use [their repository](https://hub.docker.com/r/google/nodejs/)
* Create a [DockerFile](https://github.com/JarJarMP/CodingSessions/blob/master/2015.08.18/DockerFile).
* build the image from the [DockerFile](https://github.com/JarJarMP/CodingSessions/blob/master/2015.08.18/DockerFile) and name it properly
```bash
$ docker build -t codingsessions/nodejs:20150818 .
```
* run a container from the created image
```bash
$ docker run -i -t codingsessions/nodejs:20150818 /bin/bash
```
* test nodejs in the container 
```bash
$ node
```
* I have the nodejs interactive javascript console, task finished
### Phase1 - sidenote
* Create a container which does 'nothing', but you can start/stop it - add a name to container during run command
```bash
$ docker run -i -t -d --name=mynodejs codingsessions/nodejs:20150818 /bin/bash
$ docker stop mynodejs
$ docker start mynodejs
```
### Phase2 - attach folder to container
```bash
$ docker run -i -t --volume=/home/peter/Documents/CodingSessions/2015.08.18/app_test:/app_test --name=mynodejs2 codingsessions/nodejs:20150818 /bin/bash
```
