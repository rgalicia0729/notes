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

Remove a running container

    $ docker rm -f <container id>

    $ docker rm -f <container name>    

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

Stop a container

    $ docker stop <container id>

    $ docker stop <container name>

Expose a container

    $ docker run -p <machine port>:<container port> <image name>

View container logs

    $ docker logs <container id>

    $ docker logs <container name>

View the logs of a container indefinitely

    $ docker logs -f <container id>

    $ docker logs -f <container name>

View the last n lines of logs

    $ docker logs --tail=10 -f <container id>

    $ docker logs --tail=10 -f <container name>

See the logs of the last minute

    $ docker logs --since=1m -f <container id>

    $ docker logs --since=1m -f <container name>

Docker bind mounts

    $ docker run -v <machine directory>:<container directory> <image name>

List existing volumes

    $ docker volume ls

Create a new volume

    $ docker volume create <volume name>

Mount a volume to a container

    $ docker run --mount src=<volume name>,dst=<container directory> <image name>

Delete volumes that are not being used

    $ docker volume prune

Copy files from machine to container

    $ docker cp <file path> <container id>:<path into container>

    $ docker cp <file path> <container name>:<path into container>

Copy files from container to machine

    $ docker cp <container id>:<path into container> <file path>

    $ docker cp <container name>:<path into container> <file path> 

View the images that are in the local environment

    $ docker image ls

    $ docker images

Bring an image from a repository to the local environment

    $ docker pull <image name>:<version>