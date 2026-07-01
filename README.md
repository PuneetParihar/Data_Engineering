1. We are doing Data Engineering Bootcamp from Zach wilson youtube playlist
Link: https://www.youtube.com/playlist?list=PLwUdL9DpGWU0lhwp3WCxRsb1385KFTLYE

2. For labs in this playlist, we have installed:
## 1. Docker on Vs code terminal >> wsl
    Steps for Installing docker on wsl:
        1. Install docker engine inside ubuntu: 
            get files to install: curl -fsSL https://get.docker.com -o get-docker.sh
            install files: sudo sh get-docker.sh
        
        2. sudo usermod -aG docker $USER - This commands add our current user to Docker group
            what is docker group? The Docker group is a Linux user group that lets users run Docker commands without needing sudo every time.
            When Docker is installed on Linux, it usually creates a group called docker. Members of this group can communicate with the Docker daemon (dockerd) through the Unix socket

            our current user when we checked was: echo $USER
                pparihar
        
        3. newgrp docker - is used to start a new shell session with the docker group as your active group, so that group membership changes take effect immediately without logging out and back in.

        4. Test: docker run hello-world - 
                docker - Invokes the Docker CLI (Command Line Interface).
                run:
                   Tells Docker to:
                   
                   Find the image locally.
                   Download it if it doesn't exist.
                   Create a container from that image.
                   Start the container.
                   Execute its default command.

                hello-world - The name of a Docker image published by Docker.

## 2. Downloading postgres docker image to run postgres
    docker pull postgres

## 3. docker run -d \
  --name postgres-db \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=admin123 \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  postgres:16

Explanation
Parameter	          |  Meaning
-d	                  |  Run in background
--name postgres-db	  |  Container name
POSTGRES_USER	      |  Database username
POSTGRES_PASSWORD	  |  Database password
POSTGRES_DB	Initial   |  database
-p 5432:5432	      |  Expose PostgreSQL port
postgres:16	          |  PostgreSQL image

## 4. To open postgres from container:
    docker exec -it postgres-db psql -U admin -d mydb

    docker exec - Run a command inside an already running container.

    -it - This is actually two flags:
        -i (interactive) - Keeps STDIN open so you can type commands.
        -t (terminal) - Allocates a terminal (TTY) so you get a proper shell experience.
    
    postgres-db - This is container name
    psql - postgre command line SQL client

    -U admin: Postgre user
    -d mydb: database to connect to

## 5. docker run -d \
  --name postgres \
  -e POSTGRES_USER=pparihar \
  -e POSTGRES_PASSWORD=pparihar123 \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  -v postgres_data:/var/lib/postgresql/data \
  postgres

  Explaination:
    docker run - starts a new container from image

    - d - runs in detached mode i.e. the container runs in background

    -- name - assigns a custom name to the container

    -e POSTGRES_USER=pparihar- Sets an environment variable inside the container.

    -e POSTGRES_PASSWORD=pparihar123 - creates password for the user

    -e POSTGRES_DB=mydb - creates database automatically when postgres start

    -p 5432:5432: maps port from my machine (laptop) to docker container
            Your Laptop/EC2       PostgreSQL Container
                  5432      --->       5432
    
    -v postgres_data:/var/lib/postgresql/data - creates a docker volume for persistent storage

    postgres - The Docker image to use. 

                    1. Docker downloads postgres:latest
                                   │
                                   ▼
                    2. Creates a container named "postgres"
                                   │
                                   ▼
                    3. Creates user "pparihar"
                                   │
                                   ▼
                    4. Creates database "mydb"
                                   │
                                   ▼
                    5. Sets password "pparihar123"
                                   │
                                   ▼
                    6. Maps port 5432
                                   │
                                   ▼
                    7. Creates volume postgres_data
                                   │
                                   ▼
                    8. Starts PostgreSQL in background

## 6. Now you can download dbeaver or any other SQL client using details as:
    Host: localhost
    Port: 5432
    Database: mydb
    User: pparihar
    Password: pparihar123