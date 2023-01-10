# My Docker 🐳 Notes


![Docker ](./media/Docker_Dive_Extension_inline_v1-980x538.png)



## Introduction To Docker 
 
> - **Docker is a program set of serval services , it Used to develope,package,ship,run your app on any platform**
> <br>
> - **Docker is a soluation for "it worked on my machine !. i don,t know why it don,t run on yours " it is a popualr statement between developer and client.**
> <br>
> - **Docker is more about managing your infrastructure , Docker provides a consistent way to package, ship and run your application across DTAP (Development, Testing, Acceptance, and Production) environment.**
> <br>
> - **Docker is based on the Linux kernel cgroup, namespace, and AUFS to encapsulate the process of isolation. The isolation environment that Docker creates is called a container.**
>

<br>

## Docker Vs VM 

1. ####  VM 🖥️

![vm](./media/Docker_vm-min-400x362.png)

> 1. **full copy of Guest OS is installed on top of the Host machine. These Guest os can be of few Gbs, where the hosted app is just of few Mbs**
> <br>
> 2. **Hypervisors like QEMU,virtualbox,vmware needed to manage Guest VM**
> <br>
> 3. **Heavyweight && Difficult to monitor && time taking**


2. #### Docker 🐳   

![docker](./media/Docker_docker-min-400x357.png)

> 1. **Docker engine run the image in an isolated runtime called docker container.**
>
> 2. **The application only needs to be packed with its dependencies libraries**
>
> 3. **lightweight and powerful than VM &&  easy to manage u can start a container of app image in just few seconds with few commands**


<br>


---

<br>


## Docker Architecture

![docker arch](./media/Docker-architecture.png)


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

> - **`docker pull image:tag `** or **`docker image pull image:tag`**  to pull image from remote or local docker registry
> *example :*  `docker image pull debian:latest`,  this  will pull debian image from docker hub
> <br><br>
> - **`docker image ls -a`** or **`docker images`** to list installed images
> <br><br>
> - **`docker image ls <image>`** to list spefic image or similar images with the same name 
> <br><br>
> - **`docker run <image:tag> <command>`** to run instance of docker image in isolated container
> <br>
> *example:* `docker run -it --rm debian:latest bash  `
> `-i` mean start a interactive session and redirect stdin of running image to current stdin , and `-t` mean allocate a ney tty or terminal channel or session to interactive with shell of the running system 
> <br>
> `--rm` mean you told docker engine or daemon to delete container after it exists by default any container you run didn,t be deleted  automaticly  untill you specify this flag `--rm` 
> <br><br>
> - **`docker image rm <image:tag>`** Or **`docker rmi <image:tag>`**, for deleteing images image .
> <br>
> *example:*  `docker image rm <debian:latest>`
> <br><br>
> - **`docker build --tag <image:name> /path/to/Dockerfile`** , to build image from docker 
> <br>
> *example:* **`docker build --tag crypt00o:latest . `** , where Dockerfile located in the same directory
> <br><br>
> - **`docker tag local-image:tag new-repo:tag`** , for tagging a local image to a repo
> <br><br>
> - **`docker push new-repo:tag`** , for pushing a new image or repo for docker registry
> <br><br>
> - **`docker image inspect <image:tag> `** ,get all info about spefic image   
> <br>
> *example:* `docker image inspect debian`
><br>
> - **`docker image history <image:tag>`** , docker images are made up of multiple layers to know more about an image history use this command 
> <br>
> *example:* `docker image history debian `
> - **`docker image load -i /path/to/imagefile.tar`**  , loading image form an exported container system or exported image  as tar archive
> <br><br>
> - **`docker image import -i /path/to/imagefile.tar`**  , same as above but just import  it
> <br><br>
> - **`docker image purne`** , for Removeing all images
>

>  ### How multilayered implementation works?
> - ***In docker, each image is made up of multiple layers. Docker uses Union FS to combine these layers into one final image.***
>
> - ***Union Fs has 2 purposes, (i) multiple disks can be linked to the same directory, (ii) Unionfs allows any mix of read-only and read-write branches, as well as insertion and deletion of branches anywhere in the fan-out.***
>

---

## Docker Container in Depth
> - **Docker Container can called be an runnable instance of an image running in an isolated process, you can run,start,stop,delete,attach containers  .** 

> - **`docker container run  image:tag`**  , to run instance of docker image in new isolated container
> <br>
>  *example:* `docker container run -it --rm --name crypt00o_container debian:latest bash ` , <br> where crypt00o_container is the new name of the new contianer
> <br><br>
> - **`docker contianer ls `**  ,for Listing containers 
> <br><br>
> - **`docker contianer ps `**  ,same as above command 
> <br>
> *example:* `docker container ls -a`  <br> , `-a` ir `-all` to list all containers , ls by default without any flags it display running containers only , <br> `-q` for showing containers ids only
> <br><br>
> - **`docker container start container_id`** , for Starting one or more stopped containers
> <br>
> *example:* `docker container start -i 86ebe40d8619 ` , where 86ebe40d8619 is an id of running container
> <br><br>
> - **`docker container stop contianer_id`** , for  Stoping one or more running containers
> <br><br>
> - **`docker container restart container_id `**  for Restarting one or more running containers
> <br><br>
> - **`docker container attach container_id`** ,  for attaching stdin,stdout,stderr  for a running container
> <br><br>
> - **`docker container rm container_id `**  ,  for Removeing one or more containers
> <br><br>
> - **`docker container cp container_id:/path /path/on/filesystem `**  , for copying file from a spefic path on container filesystem to spefic path on host filesystem
> <br><br>
> - **`docker container cp /path/on/filesystem container_id:/path `** , for copying file from a spefic path on host filesystem to spefic path on container filesystem 
> <br><br>
> - **`docker contianer exec container_id <new command>`**,  for Running a command inside  a running container
> <br><br>
> - **`docker contianer kill contianer_id`** , for killing a Running Container you can speficy spefic kill signal useing `--signal`  followed  with signal name or number 
> <br><br>
> - **`docker contianer pause contianer_id`** , for pauseing a running contianer 
> <br><br>
> - **`docker container unpause contianer_id`** , for run a paused  contianer
> <br><br>
> - **`docker container logs contianer_id`** , for report logs(stdin,stdout,stderr) , and you can continue track  any new changes  with `-f` or `--follow`
 flags
> <br><br>
> - **`docker container stats contianer_id`** , for displaying a live stream of container resource changes and observer Usage it (net,io,mem,cpu)
> <br><br>
> - **`docker container top container_id `** , for Display the running processes of a container 
> <br><br>
> - **`docker container  diff container_id `** , for Display changes to files or directories on a container's filesystem
> <br><br>
> - **`docker container commit contianer_id newimagename:tag`** , for Createing a new image from a container's changes
> <br><br>
> - **`docker container export contianer_id -o /path/to/outfile.tar `** ,Export a container's filesystem as a tar archive 
> <br><br>
> - **`docker container inspect contianer_id`** , to get inforamtion and current config of a spefic container
> <br><br>
> - **`docker container purne `** for deleteing all containers
>


## Docker Volumes and Data Management

![docker](./media/Docker_data-management.png)

> *By default, all files created inside a container are stored on a writable container layer. Which means:*
> <br>
> ***1. The data doesn’t persist when that container no longer exists, and it can be difficult to get the data out of the container if another process needs it.***
> <br>
> ***2. A container’s writable layer is tightly coupled to the host machine where the container is running. You can’t easily move the data somewhere else.***
> <br>
> ***3.Writing into a container’s writable layer requires a storage driver to manage the filesystem. The storage driver provides a union filesystem, using the Linux kernel. This extra abstraction reduces performance as compared to using data volumes, which write directly to the host.***
>
<br><br>

#### There are 2 ways to manage data in a container:

> ***1. Using Data Volumes – run `docker volume --help` for more info.***
<br>
> ***2. Mount host directory – Bind mounts.***
>


![types of mounting fs](./media/types-of-mounts.png)


### 1. Useing A Data Volumes
 

#### Docker Volumes 

<br>

***Volumes are stored in a part of the host filesystem which is managed by Docker (/var/lib/docker/volumes/ on Linux). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker  and can be shared with multiple containers.***

<br>

> - **`docker volume create volume_name`** , for createing a volume
> - **`docker volume ls `** , for Listing volumes
> - **`docker volume inspect volume_name`** ,for getting information about volume
> - **`docker volume rm volume_name`** , for Removeing Volumes
> - **`docker volume purne`** , for Removeing all volumes 


> - *To Use Docker volume while running container* **`--mount source=volume_name,destination=/mount_point_on_container,<optional readonly>`**
> <br>
> - *Another Way :* **`-v volumes:/mount_point_on_container`** 


> *example:*
> <br>
> `docker volume create crypt00o_volume`
> <br>
> `docker image pull debian:latest `
> <br>
> `docker container run --rm -it --name crypt00o_container --mount source=crypt00o_volume,destination=/crypto debian:latest`
> <br>
> *running volume as readonly:* `docker container run --rm -it --name crypt00o_container --mount source=crypt00o_volume,destination=/crypto,readonly debian:latest`

<br><br>

### 2.  Mount host directory

*To make a Container can read or read and write data on The Main Host* **`--mount type=bind,source=volume_name,destination=/mount_point_on_container,<optional readonly>`**

> *example:*
> <br>
> `docker volume create crypt00o_volume`
> <br>
> `docker image pull debian:latest `
> <br>
> `docker container run --rm -it --name crypt00o_container --mount source=/tmp,destination=/crypto debian:latest`
> <br>
> *running volume as readonly:* `docker container run --rm -it --name crypt00o_container --mount source=/tmp,destination=/crypto,readonly debian:latest`

## Networking With Docker 

![docker bridge net](./media/Docker_bridge_network.jpg)

> ***Mapping ports***
> <br>
> - **`-p host_port:container_port`** , to forward a port from host to container
> <br><br>
> - **`-p host_ip:host_port:container_port`** , to forward a port from spefic host or ip to container
> <br><br>
> - **`-p host_ip::container_port`** , to forward all ports of spefic host to spefic container port
> <br><br>
> - **`/tcp` or `/udp` `-p host_port:container_port/udp`** , use with all of above to determine if tcp or udp 
> <br><br>
> - **`docker port contianer_id`** , to view the current port configuration mapping, you can also view the address binding
> <br><br>


> *examples:*
> <br>
> `docker container run --rm -it --name crypt00o_container -p 80:3000 debian:latest npm start`
> <br>
> `docker container run --rm -it --name crypt00o_container -p 192.168.1.109:80:3000 debian:latest npm start`
> <br>
> `docker container run --rm -it --name crypt00o_container -p 127.0.0.1:80:3000/udp debian:latest bash`
> <br>
> `docker container run --rm -it --name crypt00o_container -p 127.0.0.1::3000 debian:latest npm start`
> <br>
> `docker port crypt00o_container`
> <br>


### Docker network Core 

> Docker’s networking subsystem is pluggable, using a specific driver. Understand which driver best suits your purpose based on the below:
> <br>
> - ***bridge – User-defined bridge networks, best for connecting multiple containers on the same host to communicate.***
> - ***host – Host networks, best when network stacks not to be isolated from the docker host.***
> - ***overlay – Overlay networks, best when multiple containers running on different hosts to communicate, or multiple applications works together using docker swarm.***
> - ***macvlan – Macvlan networks, best when migrating from a VM setup or containers need to look like physical hosts.***

#### Docker Network

> - **`docker network create -d <host|overlay|macvlan|bridge> network_name`** ,  create new network 
> <br><br>
> - **`docker network inspect network_name`**  , get network config and info 
> <br><br>
> - **`docker network ls `** , list networks
> <br><br>
> - **`docker network rm network_name`** , delete one or more network
> <br><br>
> **`docker network prune `** , delete all networks


> *example:*
> <br>
> `docker create network -d bridge crypt00o_network` , if you face any problems in iptables with your debian distro like me :D , ( cause i use kali(debian based distro) just restart the docker again by `sudo service docker restart ` and try createing docker network again . 
<br>
> `docker run --rm --name crypt00o_container -it -p 3000:4000 --network crypt00o_network debian:latest bash`



