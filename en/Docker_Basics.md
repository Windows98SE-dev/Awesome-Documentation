---
Author: Windows98SE-dev
License: CC BY 4.0
---
# Docker Basics
## Essential commands
### Docker build
Builds your docker image
```bash
docker build -t my-image:ver "Dockerfile path"
```
### Docker exec
Executes a command inside of your container

Usage
```bash
docker exec -it <CONTAINER_ID> <command>
```
Example : Access the container shell
```bash
docker exec -it <CONTAINER_ID> sh
```
Bash is fine too if the container supports it
### Docker start
Starts a container
```bash
docker start <CONATINER_ID>
```
### Docker stop
Stops a container
```bash
docker stop <CONTAINER_ID>
```
### Docker rm
Removes a stopped container
```bash
docker rm <CONTAINER_ID>
```
### Docker inspect
Generates an advanced report of informations about the container in JSON
```bash
docker inspect <CONTAINER_ID>
```
### Docker stats
Shows the usage of a container
```bash
docker stats <CONTAINER_ID>
```
### Docker logs
Display logs of a running container
```bash
docker logs <CONTAINER_ID>
```
## Volumes
### What are they ?
Docker volumes are persitent storage to keep data after a container's deletion
### Where are they stored ?
Usually in /var/lib/docker/volumes/
### How do I run a container with one ?
Create a link between the volume and the directory in the container using the -v argument
```bash
docker run -d -p <PORTS> -v my_volume:/data my-container
```
### Removing a volume
You can remove a volume by using
```bash
docker volume rm my_volume
```
You can also bulk delete volumes that aren't in use by running containers
```bash
docker volume prune
```
### Useful commands
You can inspect volumes like you can inspect containers using
```bash
docker volume inspect my_volume
```
## Bind mounts
### What are they ?
Bind mounts are sort of direct access to a folder of the host on the container, it's like a volume but it isn't a virtual disk, meaning you can explore it's contents plainly (cd, ls, cat, ...)
### How do I run a container with one ?
Put a path instead of a volume name when using the -v argument
```bash
docker run -d -p <PORTS> -v /path/on/host:/path/on/container my-container
```
### Things to know
You can force a container to have different permission to the bind mount by adding :ro (Read Only) or :rw (Read Write) to the end of the path on the container

## TMPFS
### What is it ?
TMPS or Temporary File System is a filesystem that instead of storing in a volume or a bind mount, will store the files in RAM, meaning that all of the data will be cleared at removal or reboot
### How do I run a container with one ?
Instead of using the -v argument, you use the --tmpfs argument followed by the path on the container, it is good to note that you can also use privileges switches like with bind mounts, you can also specify the size using ,size=(A numeber)(G-igs, M-egs, K-ilos, B-ytes)

NB: You can't type the - part, it is only a reference to help people understand the abreviations
```bash
docker run -d -p <PORTS> --tmpfs /path/on/my/container:rw,size=50M my-container
```
