# Docker Tutorial - Running MongoDB with Docker

This tutorial introduces Docker, explaining its key concepts, and guiding you through the steps to set up and run MongoDB inside a Docker container.

---

## Table of Contents

1. [What is Docker?](#what-is-docker)
2. [Installing Docker](#installing-docker)
3. [Hello World](#3-hello-world)
4. [Running MongoDB with Docker](#running-mongodb-with-docker)
5. [Testing](#testing-mongodb)
6. [docker compose](#5-docker-compose)

---

## 1. What is Docker?

Docker is a platform that enables developers to create, deploy, and run applications in containers. Containers are lightweight, portable units of software that package up an application and its dependencies, ensuring it runs consistently across different environments.

### Key Benefits:
- **Portability**: Docker containers run the same, regardless of where they’re deployed.
- **Isolation**: Each container is isolated from others, ensuring applications run without interference.
- **Efficiency**: Containers share the host system’s kernel, making them more lightweight than traditional virtual machines (VMs).

### Why Use Docker?

- **Consistency**: Developers can ensure that their application will work the same on any machine.
- **Easy Deployment**: Docker simplifies the deployment process by allowing you to create and share containerized apps.
- **Efficient Resource Usage**: Containers consume fewer resources than VMs since they share the same OS kernel.W

## Key Docker Concepts

Before we dive into the tutorial, here are some essential Docker terms:

- **Image**: A read-only template that contains instructions for creating a container. Images can include everything needed to run an application.
- **Container**: A running instance of a Docker image. It’s a lightweight and isolated environment for running applications.
- **Dockerfile**: A file that contains instructions to build a Docker image.
- **Docker Hub**: A public registry where you can find and share Docker images.

---

## 2. Installing Docker

To start using Docker, you need to install it on your machine.

### Install Docker:
- **For Windows** and **MacOS**: Visit [Docker Desktop](https://www.docker.com/products/docker-desktop) and follow the installation instructions.
- **For Linux**: Run the following commands:
  ```bash
  sudo apt-get update
  sudo apt-get install docker-ce docker-ce-cli containerd.io
  ```

Once installed, you can verify it by running:
```bash
docker --version
```

---

## 3. Hello World

In this tutorial, you’ll learn how to run your first container using Docker and test it with a simple "Hello World" example. This is a great way to verify that Docker is installed and working correctly on your system.

### Step 1: Running a "Hello World" Container

Docker provides a simple `hello-world` image that outputs a message to verify Docker installation.

Run the following command in your terminal:

```bash
docker run hello-world
```

#### Explanation:

- **docker run**: This command starts a new container.
- **hello-world**: The name of the Docker image. If the image is not already on your system, Docker will automatically pull it from Docker Hub.

#### What Happens Next:

- Docker will check if the `hello-world` image is available locally.
- If the image is not found, Docker will pull it from Docker Hub (an online repository of Docker images).
- Docker creates a new container using the `hello-world` image and executes the default command.
- The container prints a "Hello from Docker!" message to your terminal.

### Step 2: Understanding the Output

You should see output similar to this:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.
```

This output confirms that Docker is installed correctly and can pull and run images.

### Step 3: Listing Docker Containers

To see all running containers, use:

```bash
docker ps
```

In this case, you won't see the `hello-world` container because it exits after printing the message. To see **all containers**, including those that have exited, use:

```bash
docker ps -a
```

You should see an entry like this:

```
CONTAINER ID   IMAGE         COMMAND    STATUS                      NAMES
abcd1234efgh   hello-world   "/hello"   Exited (0) 2 minutes ago    quirky_knuth
```

- **CONTAINER ID**: The unique identifier for the container.
- **IMAGE**: The image used to create the container (`hello-world`).
- **STATUS**: The current state of the container (e.g., "Exited").

### Step 4: Cleaning Up

You can remove the `hello-world` container using the following command:

```bash
docker rm <container_id>
```

Replace `<container_id>` with the actual container ID (e.g., `abcd1234efgh`).

To remove the `hello-world` image from your system, use:

```bash
docker rmi hello-world
```

Tip: Write down the docker command that you learned so far - you'll need them again :)

---

## 4. Running MongoDB with Docker

Now, let’s set up and run  something more real world - a MongoDB container.

### 1. Pulling the MongoDB Image

Docker uses images to create containers. MongoDB’s image is available on Docker Hub.

To pull the latest MongoDB image, run:
```bash
docker pull mongo
```

This command fetches the MongoDB image and stores it locally.

### 2. Running the MongoDB Container

Once the image is pulled, you can run MongoDB in a container. Use the following command to start MongoDB:

```bash
docker run -d --name mongodb-container -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password mongo
```

Here’s what the command does:
- **`-d`**: Runs the container in the background (detached mode).
- **`--name mongodb-container`**: Assigns a name to the running container.
- **`-p 27017:27017`**: Maps port 27017 on your local machine to port 27017 in the container (MongoDB’s default port).
- **`-e MONGO_INITDB_ROOT_USERNAME=admin`** and **`-e MONGO_INITDB_ROOT_PASSWORD=password`**: Environment variables to set the MongoDB root username and password.
- **`mongo`**: The MongoDB image you pulled earlier.

To verify if MongoDB is running, list all running containers:
```bash
docker ps
```

---

## 5. Testing MongoDB

Now that MongoDB is running, you can test it by connecting with a MongoDB client or using `mongo` from another Docker container.

### Using Docker Mongo Shell
You can also connect using the `mongo` shell inside another Docker container:
```bash
docker run -it --rm --network host mongo mongo --host localhost -u admin -p password
```

---

## 6. docker compose

#### What is Docker Compose?

Docker Compose is a tool that allows you to define and manage multi-container Docker applications using a simple YAML configuration file. Instead of manually running multiple `docker run` commands, you can define your containers and their configurations in a `docker-compose.yml` file. This approach helps simplify the process of managing complex applications with multiple services, volumes, networks, and environment variables.

With Docker Compose, you can:

- Define services (e.g., MongoDB, Redis, a web app) in a single configuration file.
- Easily start, stop, and manage these services with a single command.
- Create networks and shared volumes automatically.
- Version control your container configurations for consistent deployments.

#### Creating a Docker Compose File for MongoDB

Let’s start by defining a `docker-compose.yml` file to run MongoDB. Here’s an example:

```yaml
version: "3.9"

services:
  mongodb:
    image: mongo:latest
    container_name: mongodb-container
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
    driver: local
```

##### Breakdown of the Docker Compose File

- **version**: Specifies the version of Docker Compose syntax. Version `3.9` is compatible with most recent Docker versions.
- **services**: Defines the services (containers) to be started. In this case, we have a single service named `mongodb`.
- **image**: The Docker image to use. Here, we use the official `mongo` image from Docker Hub.
- **container_name**: Sets a custom name for the MongoDB container.
- **ports**: Maps port `27017` on your local machine to port `27017` in the container (MongoDB’s default port).
- **environment**: Defines environment variables to set the MongoDB root username and password.
- **volumes**: Mounts a persistent volume for MongoDB data storage to ensure data is not lost when the container is stopped.

#### Starting MongoDB with Docker Compose

To start the MongoDB container using Docker Compose, follow these steps:

1. Ensure your `docker-compose.yml` file is in the current working directory.
2. Run the following command:

   ```bash
   docker-compose up -d
   ```

   - **up**: Starts the services defined in the `docker-compose.yml` file.
   - **-d**: Runs the services in the background (detached mode).

#### Verifying the MongoDB Container

Check if your container is running and run a command in the container.

---

## Conclusion

Congratulations! You’ve successfully set up and run MongoDB in a Docker container. This tutorial introduced Docker's basic concepts, guiding you through creating and running a MongoDB instance.