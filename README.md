# Microservices

## Containerisation with Docker!

### Why use Monolithic instead?
- Small limited scope tech. I.e a school with a fixed amount of students and users that doesn't change year on year. This doesn't need the scope to expand or scale.
- Cheaper than Microservices in the short term. ROI for Microservices is better in the long term though. 

### What is Docker?

- Docker is a containerisation platform
- Images are immutable

### Benefits
- Shares resources based on OS - VMs need their own kernel, host OS and then contents.
- Doesn't matter where you want to run it, but each container is kernel specific
- Images can be stored on localhost, in DockerHub, or in a volume (partition).
- Super fast deployment
- Version Control
- Consistent and Isolated Environment

### Commands // First time operation
- Install docker `https://docs.docker.com/desktop/windows/install/`
- Install WSL2 `https://docs.microsoft.com/en-gb/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package` and run `wsl --set-default-version 2` in Powershell
- `docker version` to find the version of docker we're using
- `docker run hello-world` we're running an image called hello-world to test our environment. The message returns: 
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:97a379f4f88575512824f3b352bc03cd75e239179eea0fecc38e597b2209f49a
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.  

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.   
    (amd64)
 3. The Docker daemon created a new container from that image which runs the    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent 
it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:      
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 ```
- `docker images` will return a list of images installed on the system
- `docker pull/push/run/create` pull, push, run (creates and starts), create (creates container but doesn't start it) an image. If the image is not found locally, it will grab it from DockerHub repo. 
- `docker rmi <image-name> -f` to remove an image. `-f` is used to force
- `alias docker="winpty docker"` this tells Windows which Docker language to use. It usually corrects the following bug: "the input device is not a TTY"
- `-p` is to connect to a particular port
- `docker run -p 2368:2368 ghost`, when we visit localhost:2368, it'll access the container. It will also return a log of everything you did in the terminal. Adding `-d` _before the -p_ will run it in detached mode and allow continued use of the terminal. Adding `--name <name>` will allow you to name a container.
- `docker ps` shows which containers are running. Adding `-a` will return a list of all images ever run.
- `docker stop <container-id>` to stop a container. It requires the container ID. When stopped, it will stop serving but hold the last used state. 
- `docker start <container-id>` to start an existing container.
- `docker rm <container-id>` will remove an existing container state
- `docker logs <container-id>` will show logs for that container if it's run in detached mode
- `docker exec -it <container-id> sh` this is essentially SSH'ing into the container. `exec` = execute, `-it` = interact, `sh` = shell. Running `bash` instead 
- `docker cp <file.name> <containerid>:<path>/<file.name>` to copy a file into a container. i.e `docker cp index.html containerid:/usr/share/nginx/html/index.html` 
- `docker commit <container-id> <username>/<name>:<tag>` to commit a new version 
`docker push <username>/<repo-name>:<tag-name>` to push to Dockerhub

### Port Mapping

i.e `docker run -d -p 4000:4000 docs/docker.github.io`
- Local Port : Native Container Port

### Playing with NGINX Container

After running `docker exec -it <container-id> sh`, we'll be inside the container.
Let's cd to /usr/share/nginx/html to find the html web page displayed on port 80.
We're inside a linux system at the moment, so run the following:
- `apt-get update -y`
- `apt-get upgrade -y`
- `apt-get install nano` we need to install the nano package in order to enter the _index.html_ file
- `nano index.html`