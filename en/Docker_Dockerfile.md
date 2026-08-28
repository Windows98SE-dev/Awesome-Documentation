---
Author: Windows98SE-dev
License: CC BY 4.0
---
# Docker: Dockerfile

## Commands

### FROM

FROM is a command that pulls an existing image from the Docker registry which will server as a base to integrate to your image.

#### Usage

```Dockerfile
FROM image:versin
```

#### Example

```Dockerfile
# Pull the Ubuntu 24.04 base image
FROM ubuntu:24.04
```

### RUN

RUN executes a command in your base while building the image

#### Usage

```Dockerfile
RUN command
```

#### Example

```Dockerfile
RUN apt update && apt upgrade && apt install node npm -y && mkdir /node
```

### COPY

Copies a local file or folder of your host inside your image

#### Usage

```Dockerfile
COPY /path/on/host /path/on/image
```

#### Example

```Dockerfile
COPY app.js /node/app.js
```

### WORKDIR

Kind of the equivalent of cd for Dockerfiles

#### Usage

```Dockerfile
WORKDIR /path/on/container
```

#### Example

```Dockerfile
WORKDIR /web
```

### EXPOSE

Opens a port on the container

#### Usage

```Dockerfile
EXPOSE port
```

#### Example

```Dockerfile
EXPOSE 3000
```

### ENV

Define environnment variables

#### Usage

```Dockerfile
ENV VARIABLE=value
```

#### Example

```Dockerfile
ENV OPENAI_TOKEN=iihjfiuwhiugiowhiu4423995829835hekjgiegibiubn
```

### CMD / ENTRYPOINT

- CMD 
    
    Defines the command to run at the start of the container

- ENTRYPOINT
    
    Defines main executable and allows parsing arguments dynamically

#### Usage

```Dockerfile
CMD ["command", "argument1", "argument2"]

ENTRYPOINT ["command", "argument"]
```

#### Example

```Dockerfile
CMD ["npm", "install"]

ENTRYPOINT ["node", "server.js"]
```

### Full Dockerfile example

This example was pulled from it-connect.fr Docker tutorial

```Dockerfile
#Base
FROM php:8.2-apache

#Define work folder
WORKDIR /var/www/html

#Copy Files
COPY index.html index.html

#Expose port
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]
```

## Building the image

To build your image, you need to run the command "docker build"

### Usage

```bash
docker build -t image-name /directory/to/Dockerfile
```

### Example

```bash
docker build -t my-webserver /project/web/
```

Then your image will be stored locally and can be found using "docker images"


