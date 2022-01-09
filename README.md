# section
1. What is docker
2. Virtual Machines vs containers
3. Architecture of docker
4. Development workflow

## What is docker
Core of what Docker is doing for you: creating a new environment that's isolated by namespace and limited by cgroups and chroot'ing you into it

## Docker Images
Pre maid docker contauners are called `image`

## Containers
Actually containers are combination of few features to achieve isolation.
1. `Chroot` is for to handle filesystem.
2. `Namespaces` is for security.
3. `Cgroup` is for resource management.

* Chroot (Change root or Linux Jail): Change root directory in linux command line 
  ```bash
  chroot /path/to/new-root-directory bash
  ```

* namespaces
Suppose if we have two chroot'd environments next to each other, they can see each other's processes. To handle this linux have 'Namespaces'. Namespaces are idea of these facets of linux where we can limit each one of prop these jails processes to write. So that each environment...

1. can write their own networ layer, change it
2. can see their own process only
3. can't mess with other environments etc.

* CGroup (control group)
Now both environments can engage in commerce in privacy and peace. But every isolated environment has access to all physical resources of the server. There's no isolation of physical components from these environments.
Google saw this same problem when building their own infrastructure and wanted to protect runaway processes from taking down entire servers
 "this isolated environment only gets so much CPU, so much memory, etc. and once it's out of those it's out-of-luck, it won't get any more."

https://btholt.github.io/complete-intro-to-containers/cgroups

## Virtual Machines vs containers

## Architecture of docker

## Development workflow

## Usefull commands
1. Build Dockerfile
```bash
docker build -t hello-docker .
```

2. Show all images
```bash
docker image ls
docker images
```

3. Run docker image
```bash
docker run hello-docker
docker run -it hello-docker // Run docker containers in interactive mode
```

4. pull docker image from docker hub
```bash
docker pull codewithmosh/hello-docker
docker run codewithmosh/hello-docker
```

5. see list of running docker containers
```bash
docker ps // to check running docker containers
docker ps -a // to check all stopped conatainers also
```

6. Open another sell in same container
```bash
docker exec -it docker-host bash
```
7. pull / push

pull allows you to pre-fetch container to run.
```bash
docker pull jturpin/hollywood
docker run -it jturpin/hollywood hollywood # notice it's already loaded and cached here; it doesn't redownload it
```
That will pull the hollywood container from the user jturpin's user account. The second line will execute this fun container which is just meant to look a hacker's screen in a movie (it doesn't really do anything than look cool.)

push allows you to push containers to whatever registry you're connected to (probably normally Docker Hub or something like Azure Container Registry).

8. inspect

```bash
docker inspect node
```
This will dump out a lot of info about the container. Helpful when figuring out what's going on with a container

9. pause / unpause

As it looks, these pauses or unpause all the processes in a container. Feel free to try

```bash
docker run -dit jturpin/hollywood hollywood
docker ps # see container running
docker pause <ID or name>
docker ps # see container paused
docker unpause <ID or name>
docker ps # see container running again
docker kill <ID or name> # see container is gone
```

10. exec

This allows you to execute a command against a running container. This is different from docker run because docker run will start a new container whereas docker exec runs the command in an already-running container.

```bash
docker run -dit jturpin/hollywood hollywood
docker ps # grab the name or ID
docker exec <ID or name> ps aux # see it output all the running processes of the container
```
If you haven't seen ps aux before, it's a really useful way to see what's running on your computer. Try running ps aux on your macOS or Linux computer to see everything running.

11. import / export

Allows you to dump out your container to a tar ball (which we did above.) You can also import a tar ball as well.

12. history

We'll get into layers in a bit but this allow you to see how this Docker image's layer composition has changed over time and how recently.

```bash
docker history node
```

13. info

Dumps a bunch of info about the host system. Useful if you're on a VM somewhere and not sure what the environment is.

```bash
docker info
```
14. top

Allows you to see processes running on a container (similar to what we did above)

```bash
docker run mongo
docker top <ID outputted by previous command> # you should see MongoDB running
```

15. rm / rmi

If you run docker ps --all it'll show all containers you've stopped running in addition to the runs you're running. If you want to remove something from this list, you can do docker rm <id or name>.

If you want to remove an image from your computer (to save space or whatever) you can run docker rmi mongo and it'll delete the image from your computer. This isn't a big deal since you can always reload it again

16. logs

Very useful to see the output of one of your running containers.

```bash
docker run -d mongo
docker logs <id from previous command> # see all the logs
```

17. restart

Pretty self explanatory. Will restart a running container

18. search

If you want to see if a container exists on Docker Hub (or whatever registry you're connected to), this will allow you to take a look.

```bash
docker search python # see all the various flavors of Python containers you can run
docker search node # see all the various flavors of Node.js containers you can run
```