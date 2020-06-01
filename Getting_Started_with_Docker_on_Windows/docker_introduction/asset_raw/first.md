

## Setting up Everything



For learning docker you can use the docker playground or you can just install the docker on your host machine. docker support windows mac and of course Linux. but in this tutorial we will use the docker playground

you can find the docker in this url

[](https://www.katacoda.com/courses/docker/playground)

install docker in linux



**`wget -q0- https://test.docker.com/ | sh`**

this command will download a  script and run the script with the bash



to find the docker version and check if the docker is installed

the command is

**`docker version`**

if everything goes right .this command will show the docker version

in your computer 



## what is Container?



![](A:\docker_introduction\first.PNG)

## virtual machine:

when you use the virtualisation manager like the hyper v, or other virtualisation software. it takes the hardware resources and then make the virtual version and then make several virtual version that we called virtual machine and on top of it we install the Operating system then on top of it the appellation run or whatever we want to do it. it takes too much resources.



## Container:

on the other hand the container like docker slices the operating system resources. every container got their root process and the own file system . they are more like operating system and it efficient to use it for it does not take a whole operating system to work.





## work with docker:

* first check if any image is installed although in  a fresh install this will show you 0

  **`docker info`**

  the output is

  ![](A:\docker_introduction\second.PNG)



* lets install a basic container name ** **hello world ****

  **`docker run hello-world`**

this command will check the local drive if the container exists if there is not then it will fetch a copy from the docker hub and and launch the container

it is a very basic container it just print some messages the output is shown bellow

![](A:\docker_introduction\third.PNG)





* To see the docker status we run this command

  **`docker ps -a`**

  ![](A:\docker_introduction\fourth.PNG)



* now if you run the command 

  **`docker info`**

  it  will show there is one container in your system

* to the see images name that is downloaded use the command

  **`docker images`**

  

## Theory behind Containers and Images

when we install the docker engine it install the docker daemon and the docker client both

two things are known as the docker engine .

when we run the command `docker run hellow-world`

this 3 thing happened behind the scene

* client make a API call to the daemon 

* Daemon implements the Docker remote Api to find the container of it is not here locally

* `docker run`  runs the new Container

  

## Working with Images

to install Alpine linux container

**`docker install Alpine`**

to install ubuntu latest

**`docker install ubuntu:latest`**

to install ubuntu image of a specific version

**`docker install ubuntu:14.04`**

to remove a docker images

**`docker rmi ubuntu:14.04`**

see the list of images

**`docker images`**

## Run a web server in Docker (NGNIX)

```bash
docker pull ngnix
docker run -d --name web_server -p 80:8080 nginx
```

**Command explanation**

**-d** tells you run the command in the detach mode (in background)

**--name** wil give you a name of the container

**-p 80:8080**  This will map the port 80 of the container to the port 8080 of the Host machine



![](A:\docker_introduction\fifth.PNG)



lets see the status

**`docker ps`**

![](A:\docker_introduction\sixth.PNG)





lets see if the server is running and we get response

from the server

```bash
curl localhost:8080
```



now if you want to interact with docker container

suppose you want to run bash  shell to do that

you can us this command

![](A:\docker_introduction\seventh.PNG)





to stop any container you use the `docker stop ` command

**`docker stop <dontainer id>`**





## Native Clustering in Docker

you can run a cluster of docker for running an app

cluster is also known as swarm

engines in a swarm run in a swarm mode manager node maintain the Swarm![](A:\docker_introduction\eight.PNG)

and just remember container also known as task



## Building a Swarm:

we will make three manager nodes and three worker nodes Manager nodes look after the state of the cluster and gives tasks to the worker nodes. you can use multiple manager nodes for redundancy . and that is also recommended that you should have at least three manager nodes in a swarm and only one leader node. manager can be a worker nodes too

Manager nodes maintain the swarm worker nodes executes the task that ae assigned to  the workers.

you can run your application in the 



1) first create a 6 instance three manager and three worker

2) go to manager1 type this command

`docker swarm init`

and to add another instance to as maanger

run this command 

`docker swarm-join manager`

it will give you a docker command with a  key. 

like this

```
docker swarm join --token SWMTKN-1-0wwpy6i65tlaw7wl12m4tir3xa7vy95ka1lufx8vhzszf1zas1-eobdc3suqm29rs6fdi64oqhxu 172.17.0.86:2377
```

copy the command

3) ssh to manager 2 and execute the command that you copy

4) go to the manager1 and execute the 

`docker swaem-join manager`

and generate another command

5) ssh to the manager3 and execute this command 

6) now for adding the worker use this command

`docker swarm-join worker`

7) now do the same process and add the other two worker

[create the command ssh to worker instance and add it]

8) to see the node use this command

`docker node ls`

9) remember manager1 will be the leader



10) sets deploy a webserver nginx. you need to deploy it as  a service

```
docker service create -p 80:80 --name webserver nginx
```

11) one thing to solve confusion is manager node is also worker node

11) now activate the rest 5

```
docker service scale webserver=5
```

12) now you can show the output with

`docker service ps`

#### now  you can hit any node in a swarm and get your service