# My Docker 🐳 Notes

## Introduction To Docker 
 
> - **Docker is a program set of serval services , it Used to develope,package,ship,run your app on any platform**
>
> - **Docker is a soluation for "it worked on my machine !. i don,t know why it don,t run on yours " it is a popualr statement between developer and client.**
>
> - **Docker is more about managing your infrastructure , Docker provides a consistent way to package, ship and run your application across DTAP (Development, Testing, Acceptance, and Production) environment.**
>
> - **Docker is based on the Linux kernel cgroup, namespace, and AUFS to encapsulate the process of isolation. The isolation environment that Docker creates is called a container.**

>

<br>

## Docker Vs VM 

1. ####  VM 🖥️

> 1. **full copy of Guest OS is installed on top of the Host machine. These Guest os can be of few Gbs, where the hosted app is just of few Mbs**
>
> 2. **Hypervisors like QEMU,virtualbox,vmware needed to manage Guest VM**
>
> 3. **Heavyweight && Difficult to monitor && time taking**


2. #### Docker 🐳   

> 1. **Docker engine run the image in an isolated runtime called docker container.**
>
> 2. **The application only needs to be packed with its dependencies libraries**
>
> 3. **lightweight and powerful than VM &&  easy to manage u can start a container of app image in just few seconds with few commands**


<br>


---

## Docker Architecture

> - ####  Docker Architecture Contain
>	1. **Docker Daemon**
>	2. **Docker client**
>	3. **Docker Registries**
>	4. **Docker Image**
>	5. **Docker Container**
>	6. **Docker Host**
>   7. **Docker Compose**
>	8. **Docker Machine**
>	9. **Docker Swarm Mode**

<br>
<br>

### 1. Docker Daemon
> - **Docker Daemon (dockerd) also called docker engine is a background process running and manages Docker images, containers, networks, and storage volumes Through a REST API .**
>

<br> 

### 2. Docker Client
> - **Docker Client almost it was cli binary which called docker , it communticate with docker Useing Commands like `docker pull` or `docker run` , This Commands sended Useing REST API  message sructure  to docker-engine (dockerd) to manage && control images, containers, networks , ...etc .**

<br> 


### 3. Docker Registry
> - **Docker Registry is the main repo  where all images are stored ,Docker Hub is the public Official Registry contain alot of images you can download and run instance of it , You Can use Docker Hub like github extacly it use pull requests and push and commits but for images you can try commands like `docker pull` and `docker run` to pull and run images directly to your machine .**

<br> 

### 4. Docker Image
> - **Docker Image is a read-only template and contains instruction for createing a Docker Container , You can inherit nad reuse base images to create a new custom image based on your needs .**
>
> - **To Create a Docker image You Should Use a file with name : Dockerfile and write dependencies and control flow inside it then run `docker build --tag <image>:<tagname> /path/to/dockerfile `**

<br> 

### 5. Docker Container
> - **Docker Container can called be an runnable instance of an image running in an isolated process, you can run,start,stop,delete,attach containers  .**

<br> 

### 6. Docker Host
> - **Docker Host is the machine which contain docker installed .**

<br> 


### 7. Docker Machine
> - **Docker Machine is a tool for provisioning and managing your Dockerized hosts (hosts with Docker Engine on them). Typically, you install Docker Machine on your local system. Docker Machine has its own command line client docker-machine --help and the Docker Engine client, docker.**

<br> 

### 8. Docker Swarm

> - **Docker uses swarm mode to manage clusters of docker-engines. Cluster is also known as Swarm. Use docker swarm --help to know the commands to manage a swarm. The popular tool Kubernetes somewhat killed this tool**

<br> 

### 9. Docker Compose

> - **Docker compose is loved by developers, to define and run multi-container docker applications. Usually, use docker-compose.yml to define the containers and use docker-compose --help commands to build, run and manage the containers. Docker compose is production ready.**

<br>

---

## Docker Image In Depth
> - **Docker image can be build form Dockerfile , are you can pull a published image from docker hub or any other docker registry.**
> <br>
> *Syntax :* `docker image <Option> <image:tag> `
> <br>
> *Run :* `docker image  --help `*for more info about usage* 

<br>

> - `docker pull image:tag ` or `docker image pull image:tag`  to pull image from remote or local docker registry
> *example :*  `docker image pull debian:latest`,  this  will pull debian image from docker hub
>
> - `docker image ls -a` or `docker images` to list installed images
><br>
> - `docker image ls <image>` to list spefic image or similar images with the same name 
><br>
>
> - `docker image run <image:tag> <command>` to run instance of docker image in isolated container
>
> *example:* `docker image run -it --rm debian:latest bash  `
> `-i` mean start a interactive session and redirect stdin of running image to current stdin , and `-t` mean allocate a ney tty or terminal channel or session to interactive with shell of the running system 
> <br>
> `--rm` mean you told docker engine or daemon to delete container after it exists by default any container you run didn,t be deleted  automaticly  untill you specify this flag `--rm` 
>
> - `docker image rm <image:tag>` Or `docker rmi <image:tag>`, for deleteing images image .
>
> *example:*  `docker image rm <debian:latest>`
>
> - `docker build --tag <image:name> /path/to/Dockerfile` , to build image from docker 
>
> *example:* `docker build --tag crypt00o:latest . ` , where Dockerfile located in the same directory
>
>
> - `docker image inspect <image:tag> ` ,get all info about spefic image   
>
> *example:* `docker image inspect debian`
>
> - `docker image history <image:tag>` , docker images are made up of multiple layers to know more about an image history use this command 
>
> *example:* `docker image history debian `
>
<br>
<br>

>  ### How multilayered implementation works?
> - ***In docker, each image is made up of multiple layers. Docker uses Union FS to combine these layers into one final image.***
>
> - ***Union Fs has 2 purposes, (i) multiple disks can be linked to the same directory, (ii) Unionfs allows any mix of read-only and read-write branches, as well as insertion and deletion of branches anywhere in the fan-out.***
>

---

## Docker Container in Depth
> - **Docker Container can called be an runnable instance of an image running in an isolated process, you can run,start,stop,delete,attach containers  .** 

> -****

