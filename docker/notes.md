# Docker

## Reference & Document
* [Runoob Tutorials](https://www.runoob.com/docker/docker-tutorial.html)
* [Docker Step by Step](https://blog.csdn.net/succing/article/details/122352867)
* [How to Write an Excellent Dockerfile](https://zhuanlan.zhihu.com/p/149529184)
* [Docker Data Persistant via VOLUME](https://baijiahao.baidu.com/s?id=1712613699393481471&wfr=spider&for=pc)
* [Docker Images Repository](https://hub.docker.com/)
* [Docker Tiers](./refer/docker_tiers.png)
* [Docker Lifecycle](./refer/docker_lifecycle.png)


## Docker Command 

### General Checking
* `version` : check docker version  
* `info` : check docker system information & number of images / containers 

* [__Reference Code__]()
```Shell
	docker info
	docker version
```

### Container Lifecycle Management
* `container` : docker container operation  
	* > `ls` : list all containers
	* > `prune` : delete useless container
* `create` : create a docker container from image, while NOT make it running  
	* > `--name` : specify name of container
* `start` : create a docker container from image & make it running  
* `stop` : stop a docker container  
* `kill` : kill a docker container  
* `restart` : restart a docker container    
* `pause` : pause a running container, while container is still visible when execute docker ps  
* `unpause` : unpaused a paused docker container    
* `rm` : remove docker container   
* `exec` : enter chosen container running in daemon model with specific command. Will NOT make container terminated when exit  
	* > `-i` : work with interaction model with container
	* > `-t` : assign a dummy terminal from container
	* > `-d` : run container in daemon model
* `run` : create a container from image, and make it running with specific command
	* > `-i` : work with interaction model with container
	* > `-t` : assign a dummy terminal from container
	* > `-d` : run container in daemon model
	* > `-P` : map container port to local machine
	* > `-p` : map container port to specific port in local machine
	* > `--name` : specify name of container

* [__Reference Code__]()
```Shell
 	# Clean all stopped containers
 	docker container prune

 	# Create a named container while not running
 	docker create --name hello-world hello-world:latest

 	# operation by contain_id
 	docker start eab78ff63369
 	docker stop eab78ff63369
 	docker restart eab78ff63369
 	docker kill eab78ff63369

 	# Container status would change from Up -> Paused & stop providing service
 	docker pause eab78ff63369
 	docker unpause eab78ff63369

 	# Remove stopped container
 	docker rm 122eb86a1929
	docker rm $(docker ps -aq)  

 	# Force remove running container
 	docker rm -f 122eb86a1929
 	docker rm -f $(docker ps -aq)  

 	# execute command in a running container
 	docker exec -it 7c95e3ff516b /bin/bash
 	docker exec -d 7c95e3ff516b echo 'Hello'
 	docker exec b34cb03be36e ps -efl

 	# Create a container using image & run command inside running container, then container would be terminated
	docker run ubuntu /bin/echo "Hello world"
	docker run ubuntu /bin/ps -elf

	# Create a container using image & dummy terminal from container for interaction & container will work under daeman model
	docker run --name hello-world hello-world:latest
	docker run -i -t ubuntu /bin/bash
	docker run -it ubuntu /bin/bash
	docker run -itd a471832/ubuntu:v1 /bin/bash
	docker run -itd --name ubuntu-alex ubuntu /bin/bash
	
	# Run container in daeman model with specified shell script
	docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
	docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"

 	# Run web application image container & map container port to local machine 127.0.0.1
 	docker run -d -P training/webapp python app.py
 	docker run -d -p 5000:5000 training/webapp python app.py
 	docker run -d -p 127.0.0.1:5001:5000 training/webapp python app.py
 	docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py
 	docker run -dp 8080:8080 springio/gs-spring-boot-docker
 	docker run -dp 8080:8080 -v todo-db:/etc/todos springio/gs-spring-boot-docker
```


### Container Management
* `ps` : list containers. By default, only running containers would be output   
	* > `--filter` : filtering output by condition
	* > `-f` : abbreviation of --filter 
	* > `-a` : all containers
	* > `-l` : the last 1 running container
	* > `-n` : the last n running containers
	* > `-q` : output in quiet model which only show container id
	* > `-s` : show size of container file	
	* > `--no-trunc` : show full container id
* `events` : check event of docker with optional specified image & timestamp   
	* > `--since` : from timestamp
	* > `--util` : to timestamp
	* > `-f` : filtering condition
* `inspect` : show detail information of chosen container   
	* > `--filter` : filtering output by condition
	* > `-f` : abbreviation of --filter 
* `top` : show detail information of chosen container   
* `stats` : list status of all running containers  
* `attach` : enter chosen container running in daemon model. make container terminated when exit  
* `port` : check port mapping of running container  
* `logs` : retrieve logs from running container  
	* > `--tail` : show last n tail log
	* > `--since` : abbreviation of --filter 
	* > `-f` : tail running log
	* > `-t` : with timestamp ahead of output log
* `export` : export a running container to a image file  
* `commit` : create a new image on top of a container & import the new image into local docker image repo
	* > `-a` : author of the new image
	* > `-m` : comments of the new image
	* > `-p` : terminate container after new image generation
	* > `-c` : use Dockerfile to create new image

* [__Reference Code__]()
```Shell
 	# docker list containers
 	docker ps -a
 	docker ps -l
 	docker ps -a -s
 	docker ps -a -q
	docker ps -n 5
 	docker ps -f status=exited
 	docker ps -f status=running
 	docker ps --filter status=exited
 	docker ps --filter status=running

	# docker event by timestamp & filtering conditions
 	docker events --since='2022-05-08'
 	docker events --until='2022-05-08'
 	docker events -f "image=hello-world:latest" --since='2022-05-08'

 	# docker inspect
 	docker inspect b34cb03be36e
 	docker inspect -f='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' b34cb03be36e
 	docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' b34cb03be36e

 	#docker check running contain status
 	docker top 122eb86a1929
 	docker stats

	# Enter chosen container running in daemon model
	docker attach 7c95e3ff516b

	# check port mapping of container
	docker port 122eb86a1929
	docker port 122eb86a1929 5000

	# export & impact docker image from running container
	docker export 90d4199eff92 > springboot_export_01.tar
	cat .\springboot_export_01.tar | docker import - springboot_restful:v1

	# generate docker image from container & import
	docker commit -a="a471832" -m="revised hellow word" 2ef47bc77b56 helloworld:v2.1

	# retrieve running container log by container id
	docker logs 90d4199eff92
	docker logs -t 90d4199eff92
	docker logs -f 90d4199eff92
	docker logs --tail 10 90d4199eff92
	docker logs --since='2022-05-08' 90d4199eff92
```

### Container rootfs Operation
* `cp` : copy & paste file between container and docker machine   
* `diff` : show file diff of contain on top of basic image   
* `volume` : copy & paste file between container and docker machine   
	* > `create` : Create a volume
  	* > `inspect` : Display detailed information on one or more volumes
  	* > `ls` : List volumes
  	* > `prune` : Remove all unused local volumes
  	* > `rm` : Remove one or more volumes

* [__Reference Code__]()
```Shell
	# copy & paste file between docker container and local machine
	docker cp .\001.txt e2ad61ad221e:/tmp/
	docker cp .\Documents\ e2ad61ad221e:/home/dts
	docker cp e2ad61ad221e:/app.jar ./

	# diff container file change on top of basic image
	docker diff e2ad61ad221e

	# create volume & run container with volume
	docker volume create todo-db
	docker run -dp 8080:8080 -v todo-db:/etc/todos springio/gs-spring-boot-docker

	# volume operation
	docker volume ls
	docker volume inspect todo-db
	docker volume rm todo-db
	docker volume prune
```


### Local Image Management
* `images` : list images in local machine docker image repo   
	* > `-a` : list all image
	* > `-q` : only show image id
	* > `-f` : filter image by key word
	* > `--digests` : show image abstract information	
	* > `--no-trunc` : show full container id
* `image` : docker image operation    
	* > `ls` : list all containers
	* > `prune` : delete useless container
* `tag` : tag existing image to have a new standalone image with different version & name     
* `history` : show historical commitment of a docker image     
	* > `-q` : only show image id
	* > `--no-trunc` : show full container id
* `rmi` : delete existing image using image id & name+tag   
	* > `-f` : force delete image with running container
* `save` : save image to local file system as an image file  
	* > `-o` : output to a file
* `load` : load an image file from local file system to local machine docker image repo   
* `import` : import a image file to local docker image repo  


* [__Reference Code__]()
```Shell
	# list docker images
	docker images
	docker images -a
	docker images -q
	docker images --no-trunc
	docker images --digests

	# list docker images with specific format
	docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.ID}}\t{{.CreatedAt}}\t{{.Size}}\t{{.Digest}}"

	# list docker images whose name is helloworld
	docker images helloworld

	# list docker images whose name is like hello*
	docker images hello*

	# list images using filtering
	docker images -f "dangling=true"
	docker images -f "label=helloworld"
	docker images -f "before=openjdk:8"
	docker images -f "since=openjdk:8"

	# list docker images
	docker image ls

	# tag existing image to have a new standalone image with different version & name
	docker tag hello-world:latest hello-world:v0.1
	docker tag helloworld:v2.1 helloworld:v2.2

	# show historical commitment of a docker image
	docker history feb5d9fea6a5
	docker history hello-world

	# remove docker image
	docker rmi 29c9f96683cf
	docker rmi helloworld:v2.1
	docker rmi -f 29c9f96683cf

	# save & load & import image from a file
	docker save -o ubunta_01.tar ubuntu:latest
	docker load --input .\ubunta_01.tar
	cat .\springboot_export_01.tar | docker import - springboot_restful:v1
```


### Remote Image Repo Management
* `login` : login remote image repo   
	* > `-u` : username
	* > `-p` : password
* `search` : search image from remote image repo   
	* > `--no-trunc` : show completed image description
	* > `--limit` : show first no. of N results
	* > `-f` : filter images by condition
* `pull` : pull image from remote image repo   
	* > `-a` : pull all tagged image
	* > `--disable-content-trust` : ignore image verification
* `push` : push image to remote image repo   
	* > `--disable-content-trust` : ignore image verification


* [__Reference Code__]()
```Shell
	# login & logout https://index.docker.io/v1/
	docker login -u sam0411 -p cosy9162A
	docker logout

	# pull image from remote docker image repo
	docker pull hello-world
	docker pull -a hello-world
	docker pull -a --disable-content-trust hello-world

	# push image to remote docker image repo
	docker push springio/gs-spring-boot-docker:latest

	# seatch image by filter
	docker search hello-world
	docker search hello-world --limit 5
	docker search --no-trunc hello-world
	docker search -f stars=10 hello-world
	docker search -f is-automated=true hello-world
	docker search -f is-official=true hello-world
	docker search --format "{{.Name}}: {{.StarCount}}" hello-world
```


### Dockerfile build
* `-t` : tag generated docker image
* `-f` : path of Dockerfile 
* `--build-arg` : specify input parameter when run Dockerfile build
* `Dockerfile Input`
	* > `FROM` : the first instruction in any valid Dockerfile and defines the base image to use as the basis for the container you're building
	* > `ARG` : defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag
	* > `LABEL` : the LABEL instruction adds metadata to an image. A LABEL is a key-value pair. To include spaces within a LABEL value, use quotes and backslashes as you would in command-line parsing
	* > `USER` : the USER instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile
	* > `WORKDIR` : the WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile. If the WORKDIR doesn’t exist, it will be created even if it’s not used in any subsequent Dockerfile instruction
	* > `EXPOSE` : the EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified
	* > `VOLUME` : the VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers, for container data persistant
	* > `COPY` : very similar to ADD, but without the compression and url functionality. According to the Dockerfile best practices, you should always use COPY unless the auto-extraction capability of ADD is needed
	* > `ADD` : simply executes commands in the container - this can be of the format of a single line to execute, e.g. RUN apt-get -y update which will be run via /bin/sh -c, or [ "executable", "param1", "param2", ... ] which is executed directly
	* > `RUN` : the RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile
	* > `CMD` : the command provides defaults for an executing container. This command will be run when the container starts up on your device, whereas RUN commands will be executed on our build servers. In a balena service, this is typically used to execute a start script or entrypoint for the user's service. CMD should always be the last command in your Dockerfile. The only processes that will run inside the container are the CMD command and all processes that it spawns
	* > `ENV` : the ENV instruction sets the environment variable <key> to the value <value>. This value will be in the environment for all subsequent instructions in the build stage and can be replaced inline in many as well. The value will be interpreted for other environment variables, so quote characters will be removed if they are not escaped
	* > `ENTRYPOINT` : configure a container that will run as an executable

 
* [__Reference Code__]()	
```Shell
	# Dockerfile 01 - Source
	FROM openjdk:8
	ARG JAR_FILE=target/*.jar
	COPY ${JAR_FILE} app.jar
	ENTRYPOINT ["java","-jar","/app.jar"]
	# Dockerfile 01 - Build
	docker build -t springboot_restful_01 .

	# Dockerfile 02 - Source
	FROM openjdk:8
	ARG JAR_FILE=spring-boot/target/*.jar
	COPY ${JAR_FILE} app.jar
	ENTRYPOINT ["java","-jar","/app.jar"]
	# Dockerfile 02 - Build
	docker build -f .\spring-boot\Dockerfile -t springboot_restful_02 .

	# Dockerfile 03 - Source
	FROM openjdk:8-jdk-alpine
	VOLUME /tmp
	ARG JAR_FILE
	COPY ${JAR_FILE} app.jar
	ENTRYPOINT ["java","-jar","/app.jar"]
	# Dockerfile 03 - Build
	docker build --build-arg JAR_FILE=target/*.jar -t springboot_restful_03 .

	# Dockerfile 04 - Source
	FROM amazoncorretto:8-alpine
	ARG JAR_FILE=service-hk-sample-web/target/*.jar
	COPY ${JAR_FILE} app.jar
	ENV JAVA_OPTS="\
	-Dspring.profiles.active=DEVELOPING \
	-Duser.timezone=Asia/Hong_Kong \
	-server \
	-Xmx1g \
	-Xms1g \
	-Xmn512m \
	-XX:SurvivorRatio=8 \
	-XX:MetaspaceSize=256m \
	-XX:MaxMetaspaceSize=512m \
	-XX:+UseParallelGC \
	-XX:ParallelGCThreads=4 \
	-XX:+UseParallelOldGC \
	-XX:+UseAdaptiveSizePolicy \
	-XX:+PrintGCDetails \
	-XX:+PrintTenuringDistribution \
	-XX:+PrintGCTimeStamps \
	-XX:+HeapDumpOnOutOfMemoryError \
	-XX:HeapDumpPath=/ \
	-Xloggc:/gc.log \
	-XX:+UseGCLogFileRotation \
	-XX:NumberOfGCLogFiles=5 \
	-XX:GCLogFileSize=10M
	"
	EXPOSE 8080
	ENTRYPOINT java ${JAVA_OPTS} -jar /app.jar #ENTRYPOINT ["java", "-jar","/app.jar"]
	# Dockerfile 04 - Build
	docker build  -t springboot_restful_04 .
```