---
Created: 2024-02-29T09:57
Class: Agility IO InternShip
Type: Back-end
Materials:
  - https://youtu.be/3c-iBn73dDE
  - https://www.docker.com/
Reviewed: true
Edited: 2025-05-10T14:46
---
> ==**Docker**== is an open platform for _developing_, _shipping_, and _running_ applications. ==**Docker**== enables you to ==separate== your applications from your infrastructure so you can deliver software quickly.

> [!info] Docker overview  
> Get an in-depth overview of the Docker platform including what it can be used for, the architecture it employs, and its underlying technology.  
> [https://docs.docker.com/get-started/overview/](https://docs.docker.com/get-started/overview/)  

---

## Installation

Here is a document for installing ==**Docker Engine**== on Ubuntu

> [!info] Install Docker Engine on Ubuntu  
> Jumpstart your client-side server applications with Docker Engine on Ubuntu.  
> [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)  

---

![[Web Technical/Docker/attachments/Untitled.png|Untitled.png]]

## Container

> [!important] A way to
> 
> ==packages== application with ==all== the necessary ==dependencies== and ==configuration  
>   
> ==It’s ==portable artifact== which easily shared.  
> It makes the development much more convenient  

![[Web Technical/Docker/attachments/Untitled 1.png|Untitled 1.png]]

### Where do container lives?

The ==container repository== is where you store your container. I could be

- Local
- Company’s private repository
- ==**DockerHub**== (a ==public repository== where developer can share ==containers== & ==images==)

### Layers of images

Basically, a container compose by layers of images.

- The first layer usually is ==**Linux Base Image**== (because it’s small)
- On top of base layer are some ==data configuration== ==layer==
- Next is ==**Applications Layers**==, it could be database(mysql, postgresql, mogodb…)

### The difference between ==**Container**== and **==Image:==**

> [!important] The
> 
> ==**Image**== is the portable part which can be shared  
> The ==**Container**== is the isolated environment which is running from a specific ==**Image**== in your machine

### Docker PORT vs Host PORT

- ==Multiple containers== can run on our **Host Machine**
- A laptop has only certain ports available
- ==Conflict on same port== on **Host Machine**

![[Web Technical/Docker/attachments/Untitled 2.png]]

The ==**Docker**== ==bind== one **Host PORT** with one **Container PORT**

```Bash
docker run -p<$HOST_PORT>:<$CONTAINER_PORT> -d <$IMAGE>:<$IMAGE_TAG>
```

---

## Deploying with Docker

Take an example that we create an application with [[NodeJS]], [[MongoDB]] and [==**Mongo Express UI**==](https://hub.docker.com/_/mongo-express)

### Docker network

While running, ==**Docker**== container create an Isolated ==**Docker**== ==network==

In this example, ==**MongoDB**== image and **==Mongo Express UI==** run in a container which connect to each other by using the ==network== name

![[Web Technical/Docker/attachments/Untitled 3.png]]

> [!important] And the
> 
> ==Node.js== application connect to the container network through the **Host PORT** `mongodb://username:password@localhost:<image-port>`

> [!important] If the
> 
> ==Node.js== application run in the same container with **==MongoDB==** and ==**Mongo-Express**== to. The `uri` will be `mongodb://username:password@<container-name>`

1. Create a network
    
    ```Bash
    docker network create mongo-network
    ```
    
2. Run the the **MongoDB** in the created network
    
    ```Bash
    docker run -d \
    	-p 27017:27017 \
    	-e MONGO_INITDB_ROOT_USERNAME=username \
    	-e MONGO_INITDB_ROOT_PASSWORD=password \
    	--name mongodb \
    	--net mongo-network \
    	mongo
    ```
    
3. Run the Mongo-Express in the created network
    
    ```Bash
    docker run -d \
      -p 8081:8081 \
    	-e ME_CONFIG_MONGODB_ADMINUSERNAME=username \
    	-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    	-e ME_CONFIG_MONGODB_SERVER=mongodb \
    	--net mongo-network \
      --name mongo-express \
    	mongo-express
    ```
    
4. Run logs
    
    ```Bash
    docker logs mongo-express
    # or 
    docker logs mongo-express -f
    ```
    

---

## Docker Compose

This is same as the command above which we you to run the ==**MongoDB**== ==container== & ==**Mongo-Express**== ==container==

```YAML
version: '3'
services:
	mongodb:
		image: mongo
		ports: 
			- 27017:27017
		environment:
			- MONGO_INITDB_ROOT_USERNAME=username
			- MONGO_INITDB_ROOT_PASSWORD=password
	mongo-express:
		image: mongo-express
		ports: 
			- 8081:8081
		environment:
			- ME_CONFIG_MONGODB_ADMINUSERNAME=username
			- ME_CONFIG_MONGODB_ADMINPASSWORD=password
			- ME_CONFIG_MONGODB_SERVER=mongodb
```

Run:

```Bash
docker-compose -f mongo.yaml up -d
```

Stop:

```Bash
docker-composr -f mongo.yaml down
```

---

## ==Dockerfile==

==**Dockerfile**== is a blueprint for creating ==**Docker**== ==Image==

```Plain
install node

set MONGO_DB_USERNAME=name
set MONO_DB_PASSWORD=pass

create "/home/app" folder

copy current from folder of host to "/home/app" (except files in .dockerignore)

start the app with "$ node /home/app/server.js"
```

```Docker
FROM node

ENV MONGO_DB_USERNAME=name \
		MONGO_DB_PASSWORD=pass

RUN mkdir /home/app

COPY . /home/app

CMD ["node","/home/app/server.js"]
```

Run the ==**Dockerfile**==

```Bash
docker build -t my-app:1.0 .
```