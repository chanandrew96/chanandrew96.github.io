---
layout: page
title: RedHat & Docker
subtitle: Set up RedHat and Docker
---

# Environment
- RedHat (RHEL 9)
    - yum
- Docker (Mirantis Container Runtime)
- Virtual Box

## RedHat Package
- net-tools
    - `ifconfig` (Check IP Address)

# Linux Commands
- Search for the package which provided the commands / exec
    - `yum provides <Command-Exec>`
- Install package
    - `yum -y install <Package-Name>`
- Check any directory/files owned by unknown user 
    - `find [directory] -nouser -ls`
- Check any directory/files owned by unknown group
    - `find [directory] -nogroup -ls`

# Docker
## Pull Images
When we pull the docker images, docker (overlay2, if you are using overlay2) will create folders under the `.GraphDriver.Data` directories  
We can inspect those directory path by executing the command `docker inspect <Image-ID>`  

## Docker Compose
### Installation
1. Download the Docker Compose executable from [Docker Compose GitHub Release](https://github.com/docker/compose/releases)  
  In case you have no idea which version should you download, use command `uname -m` to check your OS architecture
    > Used Docker Compose v2.26.1 in below steps
2. Place and rename the executable to `/usr/local/bin/docker-compose`
3. Create symbolic link  
    ``` shell
    ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose 
    ```
4. Give execute permission
    ``` shell
    chmod +x /usr/local/bin/docker-compose
    ```
5. Check docker compose ready
    ``` shell
    docker-compose --version
    Output:
    Docker Compose version v2.26.1
    ```
### Start the docker container with `docker-compose.yml` file
1. Create your docker compose project folder
    ``` shell
    mkdir <Project-Name>
    ```
2. Copy or Create `docker-compose.yml` file inside the project folder
3. Start the container (Image not exist in local will automatically download when start)
    ``` shell
    docker-compose -f <docker-compose.yml> up -d
    ```
    > -f: Specific the yml file to start  
    > -d: Start the container in background


#### Troubleshoot on docker-compose
- "Project name not found" error
    - You must locate the `docker-compose.yml` under the project folder, which the folder name will be used as **Project Name**
    - Reference Link: [WITH DOCKER using compose gives "Project name not found"](https://github.com/earthly/earthly/issues/3164)
- "name does not match pattern" error
    - The folder name was default as the project name, so place the `docker-compose.yml` file under the project folder match the pattern could fix the issue
    - Reference Link: ['name' does not match any of the regexes: '^x-' while trying to set the project name in a docker-compose.yml](https://stackoverflow.com/a/73427527/5629361)

## Inspect the Docker Image
You can check how the Docker Image built by using the [`docker history`](https://docs.docker.com/reference/cli/docker/image/history/) command  
``` shell
docker history <Docker-Image> -H --no-trunc
```
Sometimes, there are directories created by the Docker Image and given unknown UID or GID. You could trace and prove by checking the docker image built process.