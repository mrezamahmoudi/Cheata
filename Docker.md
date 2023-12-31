
# General Commands

#### Shows the Docker version inform­ation

> docker version
#### Display system­-wide inform­ation

> docker info
#### Shows help for a specific command

> docker help <co­mma­nd>


# Image Commands

#### List images

> docker images
#### Pull an image or a repository from a registry

> docker pull <im­age>
#### Remove one or more images

> docker rmi <im­age>


# Container Commands

#### Lists running containers

> docker ps
#### List all containers (both running and stopped)

> docker ps -a
#### Run a command in a new container

> docker run <im­age>
#### Start one or more stopped containers

> docker start
#### Restart one or more containers

> docker restart
#### Stop one or more running containers

> docker stop <co­nta­ine­r>
#### Remove one or more containers

> docker rm <co­nta­ine­r>
#### Rename a container

> docker rename

# Dockerfile Instru­ctions

#### Set the Base Image for subsequent instru­ctions

> FROM
#### Execute any commands in a new layer on top of the current image and commit the results

> RUN
#### Provide defaults for an executing container

> CMD
#### nform Docker that the container listens on the specified network ports at runtime

> EXPOSE
#### Set enviro­nment variables

> ENV
#### Copy new files, direct­ories or remote file URLs from <sr­c> and add them to the filesystem of the image at the path <de­st>

> ADD
#### Copy new files or direct­ories from <sr­c> and add them to the filesystem of the container at the path <de­st>

> COPY
#### Allows you to configure a container that will run as an executable

> ENTRYPOINT
#### Create a mount point with the specified name and mark it as holding externally mounted volumes from native host or other containers

> VOLUME
#### Set the user name or UID to use when running the image and for any RUN, CMD and ENTRYPOINT instru­ctions that follow it in the Dockerfile

> USER
#### Sets the working directory for any RUN, CMD, ENTRYP­OINT, COPY and ADD instru­ctions that follow it in the Dockerfile

> WORKDIR


# Dockerfile Commands

#### Build an image from a Dockerfile in the current directory

> docker build -t <ta­g>
#### Tag an image to a name (local or registry)

> docker tag <im­age> <ta­g>