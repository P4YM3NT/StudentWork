
# Tutorial: Part 1 – Introduction and Setup

In this section, we will set up and configure the essential tools and technologies we will use. The goal is to establish a development environment for web development with **Vue.js**, **Docker**, and **PostgreSQL**. Let's go step-by-step!

---

## 1. Introduction to the Technologies
Before we start the setup, let's get a brief overview of what each technology does:

1. **Vue.js**: A progressive JavaScript framework used for building user interfaces. It is easy to learn and offers a powerful syntax for creating dynamic web applications.
2. **Docker**: A platform for containerizing applications, allowing you to run and distribute your applications and services in isolation.
3. **PostgreSQL**: A powerful, open-source object-relational database management system (DBMS) known for its stability and extensive features.

---

## 2. Prerequisites
Before you begin, make sure you have the following programs installed on your system:

1. **Node.js** (version 16 or higher)
2. **npm** (automatically installed with Node.js)
3. **Docker** and **Docker Compose**
4. **PostgreSQL** (optional if you do not want to run it via Docker)

### Checking the Installation
Open your terminal (or command prompt) and enter the following commands to ensure everything is installed correctly:

```bash
node -v
npm -v
docker -v
```

If you see all the versions correctly, you are ready to go!

---

## 3. Setting Up Vue.js Development Environment

### 3.1. Installing Vue CLI
Vue CLI is a command-line tool that makes setting up and developing Vue.js projects easier.

```bash
npm install -g @vue/cli
```

> **Note**: The `-g` flag means the package is installed globally on your system.

### 3.2. Creating a New Vue Project
Run the following command to create a new Vue project:

```bash
vue create my-project
```

You will be prompted to choose a configuration. For this tutorial, select **manual configuration** and enable the following options:

- **Babel** (for modern JavaScript syntax)
- **Router** (if you plan to have a multi-page application)
- **Vuex** (optional, if you need to manage a global state)

Once the selection is complete, Vue CLI will set up your project.

### 3.3. Understanding the Project Structure
Navigate to your project directory:

```bash
cd my-project
```

The essential project structure looks like this:

- **src/**: This contains the main code of your application.
  - **components/**: Components you can create and reuse.
  - **App.vue**: The main component of the application.
  - **main.js**: The entry point of your Vue.js application.
- **public/**: Static files, such as images or the `index.html` file.
- **package.json**: Contains information about your project’s dependencies and scripts.

### 3.4. Running the Application
To run your application in development mode, use:

```bash
npm run serve
```

Open your browser and go to `http://localhost:8080`. You should see the default Vue.js welcome page. Congratulations, your Vue project is now set up!

---

## 4. Installing and Configuring Docker

### 4.1. Download and Install Docker
- Visit the [official Docker website](https://www.docker.com/get-started) and download Docker Desktop.
- Follow the installation instructions for your operating system (Windows, macOS, or Linux).

### 4.2. Checking Docker
After installation, you can verify that Docker is installed correctly by running:

```bash
docker --version
```

### 4.3. Installing Docker Compose (if not included with Docker Desktop)
Docker Compose is a tool for running multi-container Docker applications. It is usually included with Docker Desktop. You can verify the installation with:

```bash
docker-compose --version
```

If Docker Compose is not installed, follow the [official instructions](https://docs.docker.com/compose/install/).

---

## 5. Configuring PostgreSQL

### 5.1. Installing PostgreSQL Locally (Optional)
If you want to use PostgreSQL locally, you can download and install it from the [PostgreSQL website](https://www.postgresql.org/download/).

- During the installation, you will be asked to create a user and password. Make sure to remember these credentials as you will need them later.

### 5.2. Using PostgreSQL with Docker (Recommended)
Using PostgreSQL with Docker is easier because it is isolated and portable.

Create a directory for your project, and create a `docker-compose.yml` file with the following content:

```yaml
version: '3.8'
services:
  db:
    image: postgres
    container_name: postgres_container
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: my-database
    ports:
      - "5432:5432"
```

Save the file and start PostgreSQL with Docker:

```bash
docker-compose up -d
```

Your PostgreSQL database will now be running in a Docker container on port 5432.

---

## 6. Summary
In Part 1, you have:
- Learned about the key tools and technologies.
- Created a Vue.js application using Vue CLI.
- Installed Docker and Docker Compose and set up a PostgreSQL database.

You are now ready to develop your frontend and backend components and connect them to the database. In the upcoming parts, we will expand our knowledge and create a complete web application.

Let me know if you have any questions or are ready to continue!
