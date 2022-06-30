# Comandos de Docker

See docker version

    $ docker --version

View docker status

    $ docker info

Run a container

    $ docker run <image name>

See the containers running

    $ docker ps

See all containers

    $ docker ps -all

    $ docker ps -a

Get information from a container

    $ docker inspect <container id>

    $ docker inspect <container name>

Name a container

    $ docker run --name <container name> <image name>

Rename a container

    $ docker rename <current name> <new name>

Remove a container

    $ docker rm <container id>

    $ docker rm <container name>

Remove all containers that are not running

    $ docker container prune

Run a container in interactive mode

    $ docker run -it <image name>

Run a container in the background

    $ docker run --detach <image name>

    $ docker run -d <image name>

Run a container with a custom command

    $ docker run -d <image name> <custom command>

Connect to a running container

    $ docker exec -it <container id> <custom command>

    $ docker exec -it <container name> <custom command>
