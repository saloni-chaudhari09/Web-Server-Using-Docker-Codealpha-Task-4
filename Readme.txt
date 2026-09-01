DOCKER WEB SERVER

Project Overview
----------------
This project demonstrates the deployment of a web server inside a Docker container using Nginx.

The web server is deployed on an AWS EC2 instance running Amazon Linux 2023. Docker is used to containerize the web application, while Nginx serves the HTML website.


PROJECT OBJECTIVES
------------------
- Learn Docker containerization basics
- Deploy and manage a web server inside Docker
- Understand Docker container lifecycle and commands
- Monitor container health and resource usage
- Troubleshoot common Docker issues
- Understand container-based application deployment best practices


TECHNOLOGIES USED
-----------------
- AWS EC2
- Amazon Linux 2023
- Docker
- Nginx
- HTML5
- Linux
- Git & GitHub


PROJECT ARCHITECTURE
--------------------

                    INTERNET
                       |
                       v
                AWS EC2 Instance
              Amazon Linux 2023
                       |
                       v
                    Docker
                       |
                       v
                Docker Container
                  web-server
                       |
                       v
                     Nginx
                       |
                       v
                  index.html
                       |
                       v
                  Web Browser


PROJECT STRUCTURE
-----------------

docker-web-server/
|
|-- Dockerfile
|-- .dockerignore
|-- README.md
|
|-- html/
    |
    |-- index.html


DOCKERFILE
----------

The Dockerfile uses the lightweight Nginx Alpine image.

FROM nginx:alpine

COPY html/index.html /usr/share/nginx/html/index.html

EXPOSE 80

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD wget --spider -q http://localhost/ || exit 1


DOCKERFILE EXPLANATION
----------------------

FROM nginx:alpine
Uses Nginx as the web server.

COPY
Copies the HTML website into the Nginx web directory.

EXPOSE 80
Documents the port used by the Nginx web server.

HEALTHCHECK
Checks whether the Nginx web server is responding correctly.


BUILD DOCKER IMAGE
------------------

Command:

docker build -t docker-web-server:v2 .

Verify the image:

docker images


RUN DOCKER CONTAINER
--------------------

Command:

docker run -d --name web-server -p 8080:80 docker-web-server:v2


PORT MAPPING
------------

EC2 Host Port 8080
        |
        v
Container Port 80
        |
        v
      Nginx


VERIFY CONTAINER
----------------

Command:

docker ps

The expected container status is:

web-server
Up
healthy

Check the health status:

docker inspect --format='{{.State.Health.Status}}' web-server

Expected result:

healthy


ACCESS THE WEBSITE
------------------

The website can be accessed using:

http://EC2-PUBLIC-IP:8080

The AWS Security Group must allow inbound TCP traffic on port 8080.


CONTAINER LIFECYCLE
-------------------

Stop the container:

docker stop web-server

Start the container:

docker start web-server

Restart the container:

docker restart web-server

View running containers:

docker ps

View all containers:

docker ps -a


CONTAINER MONITORING
--------------------

View container logs:

docker logs web-server

Monitor CPU and memory:

docker stats web-server

View detailed container information:

docker inspect web-server

Check container health:

docker inspect --format='{{.State.Health.Status}}' web-server


TROUBLESHOOTING
---------------

PORT CONFLICT

A port conflict was intentionally tested by attempting to run another
container using port 8080.

Command:

docker run -d --name test-server -p 8080:80 nginx:alpine

Docker reports that the port is already allocated because the
web-server container is already using port 8080.

SOLUTION

Use another host port:

docker run -d --name test-server -p 8081:80 nginx:alpine

After testing, the temporary container can be removed:

docker stop test-server

docker rm test-server


DOCKER DEPLOYMENT BEST PRACTICES
--------------------------------

The following practices were implemented:

- Used lightweight nginx:alpine image
- Added Docker HEALTHCHECK
- Used versioned Docker image tags
- Created a .dockerignore file
- Used a simple project structure
- Monitored container health
- Monitored CPU and memory usage
- Practiced Docker container lifecycle commands
- Tested and resolved a port conflict


FINAL RESULT
------------

A professional HTML website was successfully deployed inside an
Nginx Docker container running on an AWS EC2 Linux server.

The complete deployment flow is:

HTML Website
     |
     v
Dockerfile
     |
     v
Docker Image
     |
     v
Docker Container
     |
     v
Nginx Web Server
     |
     v
AWS EC2
     |
     v
Internet


TASK REQUIREMENTS COMPLETED
----------------------------

1. Learn Docker containerization basics
   COMPLETED

2. Deploy and manage a web server inside Docker
   COMPLETED

3. Understand container lifecycle and commands
   COMPLETED

4. Monitor container health and troubleshoot issues
   COMPLETED

5. Explore container-based application deployment best practices
   COMPLETED


INTERNSHIP PROJECT
------------------

Task 4: Web Server Using Docker

Technologies:

AWS EC2
Amazon Linux 2023
Docker
Nginx
HTML
Linux
Git & GitHub


FINAL OUTCOME
-------------

A containerized Nginx web server was successfully deployed on AWS EC2
using Docker.

The container is health-monitored, managed using Docker lifecycle
commands, and accessible through the EC2 public IP.