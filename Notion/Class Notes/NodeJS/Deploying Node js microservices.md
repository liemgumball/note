
<aside>
💡 **Node.js** microservices commonly expose **RESTful APIs**. 
**REST** stands for **Representational State Transfer**

</aside>

## Target

- Generating a microservice with **LoopBack**
- Handling errors
- Building a **Docker** container
- Publishing a **Docker** image
- Deploying to **Kubernetes**

---

## Generating microservice with LoopBack

1. Install **Loopback CLI**
    
    ```bash
    npm install --global @loopback/cli
    ```
    
2. Generating the project, we call the **LoopBack CLI**, providing a project name
    
    ```bash
    lb4 loopback-bookstore
    ```
    
    Entering the command will start an interactive interface where the **LoopBack CLI** will request information for your new project. **CLI** question asks the user which features should be enabled in the project.
    
    ![Untitled](Notion/Class%20Notes/NodeJS/Deploying%20Node%20js%20microservices/Untitled.png)
    
3. The **LoopBack CLI** has now generated the application.
    
    ![Untitled](Notion/Class%20Notes/NodeJS/Deploying%20Node%20js%20microservices/Untitled%201.png)
    
4. Now using **LoopBack's** model generator. Enter the following command to start creating a model
    
    ```bash
    lb4 model
    ```
    
    ![Untitled](Notion/Class%20Notes/NodeJS/Deploying%20Node%20js%20microservices/Untitled%202.png)
    
5. Now that we've created our model, we need to create our data source
    
    ```bash
    lb4 datasource
    ```
    
    ![Untitled](Notion/Class%20Notes/NodeJS/Deploying%20Node%20js%20microservices/Untitled%203.png)
    
6. Next, we need to create a repository. This is a class that binds the data source and the model.
    
    ```bash
    lb4 repository
    ```
    
    ![Untitled](Notion/Class%20Notes/NodeJS/Deploying%20Node%20js%20microservices/Untitled%204.png)
    
7. Now, we need to create a controller. A controller handles the **API** requests and responses. Our controller should be a **REST Controller with CRUD functions**.
    
    ```bash
    lb4 controller
    ```
    
8. Run the service
    
    ```bash
    yarn start
    ```
    

### There's more…

**GraphQL** is an **API** query language that enables consumers of an **API** to define the data they want to receive from a request. With **GraphQL**, a request is sent to a single endpoint with a query, and the endpoint manipulates the data into the form requested.

<aside>
💡 **GraphQL** **APIs** are recommended over **RESTful APIs** in situations where there is a need for greater flexibility in the data requested.

</aside>

1. Run the service
    
    ```bash
    yarn start
    ```
    
2. In a new Terminal window, enter the following command
    
    ```bash
    npx openapi-to-graphql-cli --port=3001 http://localhost:3000/openapi.json
    ```
    
    This command instructs the `openapi-to-graphql-cli` module to read the **OpenAPI** specification from our **LoopBack** application. The module will create and host a corresponding **GraphQL** endpoint on port 3001. Under the covers, `openapi-to-graphql-cli` is using **Express.js** to host the **GraphQL** endpoint.
    

### Handling errors

<aside>
💡 In *microservice architectures*, you will have many applications communicating together to form a larger system. When you have a system formed of many moving parts, it's important to handle errors within the system appropriately.

</aside>

---

## Building a [Docker](Docker.md) container

Once we have a **Node.js** *microservice*, we need to package it ready for deployment to the cloud. Cloud and container technologies go hand in hand, and one of the most prevalent container technologies is **Docker**.

<aside>
💡 **Docker** is a tool designed to make it easier to *create*, *deploy*, and *run applications* using containers. A container enables you to package up your application with all its *dependencies*. A container is often said to be like a virtual machine, the key difference being that **Docker** allows applications to reuse the same **Linux kernel**, whereas a virtual machine virtualizes the whole **OS**.

</aside>

1. Ensure Docker is running
    
    ```bash
    docker -v
    # or
    sudo service status docker
    # or
    docker run hello-world
    ```
    
2. Generate a sample **API** in a new directory named `fastify-microservice`
    
    ```bash
    npx fastify-cli generate fastify-microservice
    cd fastify-microservice
    ```
    
3. Creating a `Dockerfile` file and a `.dockerignore` file in the `fastify-microservice` directory
    
    ```docker
    FROM node:14
    
    WORKDIR "/app"
    
    RUN apt-get update \
    		&& apt-get dist-upgrade -y \
    		&& apt-get clean \
    		&& echo 'Finished installing dependencies'
    
    COPY package*.json ./
    
    RUN npm install --production
    
    COPY . /app
    
    ENV PORT 3000
    
    EXPOSE 3000
    
    USER node
    
    CMD ["npm", "start"]
    ```
    
    ```
    .git
    .gitignore
    node_modules
    npm-debug.log
    ```
    
4. We're now ready to build the *microservice*. We do this by using the `docker build` command along with `fastify-microservice` as a tag for our image
    
    ```bash
    docker build --tag fastify-microservice .
    ```
    
5. List all of your **Docker** *images*. You should expect to see the `fastify-microservice` **Docker** *image* in the list
    
    ```bash
    docker images
    ```
    
6. Run the **Docker** *image* as a **Docker** *container*, passing the `--publish` flag to instruct **Docker** to map `port` 3000 from within the container to port 3000 on our local machine.
    
    ```bash
    docker run --publish 3000:3000 fastify-microservice
    ```
    

---

## Publishing a Docker image

[**Docker Hub**](http://hub.docker.com) provides a global repository of images

1. Create a **Docker Hub** account
2. Authenticate your **Docker** client
    
    ```bash
    docker login
    ```
    
3. Once we have authenticated our **Docker** client, we then need to retag our image for it to be pushed to **Docker Hub**
    
    ```bash
    docker tag fastify-microservice <namespace>/fastify-microservice
    ```
    
4. Push the newly tagged image
    
    ```bash
    docker push <namespace>/fastify-microservice
    ```
    

---

## Deploying to [**Kubernetes**](https://kubernetes.io/)

[**Kubernetes](https://kubernetes.io/docs/concepts/overview/),** also known as **K8s**, is an open-source system developed by **Google** for *automating deployment*, *scaling*, and *management* of containerized applications

**Kubernetes** is a *comprehensive* and *complex* tool that provides the following features, among others:

- Service discovery and load balancing
- Storage orchestration
- Automated rollouts and rollbacks
- Automatic bin packing, specifying how much CPU and memory each container needs
- Self-healing
- Secret and configuration management