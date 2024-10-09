### Docker Compose  
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration. Compose works in all environments: production, staging, development, testing, as well as CI workflows.

**Docker Desktop** includes Docker Compose along with Docker Engine and Docker CLI, which are Compose prerequisites.

#### Following are the use cases of Docker Compose:
- Development environments
- Automated testing environments
- Single host deployments

---

### Docker Compose Key Features
- Have multiple isolated environments on a single host.
- Preserves volume data when containers are created.
- Only recreates containers that have changed.
- Supports variables and moving a composition between environments.

---

### Example of `docker-compose.yml`
```yaml
services:
  web:
    image: "nginx"
  redis:
    image: "redis:6.0-alpine3.18"
```

---

### Commands
- **`docker compose --help`**  
  This command is used to see other available commands.

- **`docker compose up`**  
  This command will take the `docker-compose.yml` file and start building containers. It will download/pull required images and create/start the necessary containers. If we modify the `docker-compose.yml` file and run `docker compose up` again, it will only recreate modified containers.

- **`docker compose up -d`**  
  Same as `docker compose up` but runs in the background, which means it won't occupy the terminal.

- **`docker compose ps`**  
  This command is used to list currently running services.

- **`docker compose exec service_name mysql -u root -p`**  
  This command is used to access the terminal of a container.

- **`docker compose stop`**  
  This command is used to stop services started using `docker compose up -d`.<br>
  Use this command when you want to temporarily stop the services but keep the containers, networks, and volumes intact for future use.
  
- **`docker compose down`**  
  Stops and removes all containers, networks, and volumes defined in the docker-compose.yml file.<br>
  Use this command when you want to completely clean up your application, removing all resources created by the docker compose up command.


### Creating `docker-compose.yml` file (09:42)
To create a `docker-compose.yml` file, you need to define the services and configurations for your application. For example, a simple file to set up a web and Redis service might look like this:

```yaml
version: '3'
services:
  web:
    image: "nginx"
  redis:
    image: "redis:6.0-alpine3.18"
```

This file specifies that Docker should pull the Nginx image for the web service and the Redis image for Redis service.

---

### Define Services (12:00)
In Docker Compose, services are the building blocks of your application. Each service represents a container in your application. You define a service in the `docker-compose.yml` file:

```yaml
services:
  db:
    image: "mysql:5.7"
    environment:
      MYSQL_ROOT_PASSWORD: example
```

This defines a `db` service using the MySQL image, and we are setting an environment variable for the root password.

---

### Check Docker Compose Version (14:55)
To check the installed version of Docker Compose, run the following command in the terminal:

```bash
docker compose version
```

---

### Check Docker Compose Help (15:11)
To list all available commands and options for Docker Compose, use the `--help` flag:

```bash
docker compose --help
```

---

### Check Docker Compose Config (17:12)
The `docker compose config` command helps you validate the `docker-compose.yml` file. It checks the file for syntax errors and displays the effective configuration:

```bash
docker compose config
```

---

### Create and Start Containers (18:27)
Use the `docker compose up` command to create and start containers as defined in your `docker-compose.yml` file:

```bash
docker compose up
```

To run it in the background (detached mode), use:

```bash
docker compose up -d
```

---

### List Containers (20:32)
To list all containers, both running and stopped, use:

```bash
docker ps -a
```

---

### List Networks (21:14)
Docker Compose automatically creates a default network for your application. To list all networks:

```bash
docker network ls
```

---

### List Volumes (21:26)
To list all volumes created in Docker:

```bash
docker volume ls
```

---

### List Running Containers (22:10)
To list only the running containers:

```bash
docker compose ps
```

---

### Execute Command Inside Service (22:27 & 52:27)
To run a command inside a running service's container, use the `docker compose exec` command:

```bash
docker compose exec <service_name> <command>
```

For example, to access the shell in a running MySQL service:

```bash
docker compose exec db mysql -u root -p
```

---

### Stop Docker Compose (23:00)
To stop running containers in Docker Compose, use:

```bash
docker compose stop
```

---

### Remove All Containers (23:12)
To remove all stopped containers and resources created by `docker compose up`, use:

```bash
docker compose down
```

---

### How to Use Environment Variables (23:43)
You can use environment variables in the `docker-compose.yml` file by using the `environment` key or by using `.env` files. Example:

```yaml
services:
  web:
    image: "nginx"
    environment:
      - APP_ENV=production
      - DEBUG=0
```

---

### Verify Variable Value (25:09)
To verify the value of an environment variable inside a container, you can execute the following command:

```bash
docker compose exec <service_name> env
```

---

### Set Environment Attribute in Service Container (25:53)
Instead of hardcoding environment variables in the `docker-compose.yml` file, you can use the `env_file` attribute to specify a file containing environment variables:

```yaml
services:
  web:
    image: "nginx"
    env_file:
      - .env
```

---

### Use Environment File in Service Container (28:30)
Environment variables can be loaded from an external file. Create a `.env` file with key-value pairs:

```
APP_ENV=production
DEBUG=0
```

Then refer to this file in your `docker-compose.yml`:

```yaml
env_file:
  - .env
```

---

### Set Profile Name for Service (30:09)
Profiles allow you to selectively run services. You can specify profiles for services in the `docker-compose.yml` file:

```yaml
services:
  web:
    image: "nginx"
    profiles:
      - web
  db:
    image: "mysql:5.7"
    profiles:
      - db
```

Run a profile with:

```bash
docker compose --profile web up
```

---

### Exposing Port (34:28)
Expose a port from a container to the host machine using the `ports` directive:

```yaml
services:
  web:
    image: "nginx"
    ports:
      - "8080:80"
```

This maps port 8080 on the host to port 80 inside the container.

---

### Set Custom Network and Network Driver (37:22)
You can define custom networks and specify the network driver in Docker Compose:

```yaml
networks:
  custom_network:
    driver: bridge

services:
  web:
    image: "nginx"
    networks:
      - custom_network
```

---

### `depends_on` - Set Order of Container Creation and Removal (40:50)
You can specify service dependencies with `depends_on`. This ensures that one service starts before another:

```yaml
services:
  web:
    image: "nginx"
    depends_on:
      - db
  db:
    image: "mysql:5.7"
```

---

### Multiple Compose Files (43:07)
You can extend your `docker-compose.yml` setup by using multiple files:

```bash
docker compose -f docker-compose.yml -f docker-compose.override.yml up
```

---

### Run Custom Compose File (44:38)
To run a specific compose file, use the `-f` flag:

```bash
docker compose -f custom-compose.yml up
```

---

### Use Custom Image Dockerfile within Compose File (46:37)
To build an image from a Dockerfile in your `docker-compose.yml` file, use:

```yaml
services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
```

---

### Docker Compose File Properties (53:31)
The main properties in a `docker-compose.yml` file include:
- **version**: The version of the Compose file.
- **services**: Define individual containers.
- **networks**: Specify networks.
- **volumes**: Specify volumes.
- **ports**: Map ports between the container and the host.

---

### Docker Compose Official Documentation (58:20)
The official Docker Compose documentation is available at:  
[https://docs.docker.com/compose](https://docs.docker.com/compose)