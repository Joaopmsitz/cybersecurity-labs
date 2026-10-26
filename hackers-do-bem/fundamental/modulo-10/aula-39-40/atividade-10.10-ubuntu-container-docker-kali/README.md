# Activity 10.10 — Running Ubuntu in a Docker Container on Kali Linux

## Objective

Use **Docker** on Kali Linux to download an Ubuntu image, create and run containers, access an interactive shell, and monitor runtime information using the `docker top` and `docker stats` commands.

At the end of the activity, the container used in the lab was stopped and inactive containers were removed.

---

## Environment

- **Operating system:** Kali GNU/Linux Rolling
- **Container image:** Ubuntu
- **Runtime:** Docker
- **Main container:** `MeuContainer`
- **Terminal:** Bash

---

## 1. Verifying Docker

Administrative privileges were obtained in the terminal:

```bash
sudo -i
```

Next, the following command was executed:

```bash
docker
```

The command displayed the Docker help screen:

```text
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Authenticate to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds and cache
  buildx*     Manage Docker Buildx
  container   Manage containers
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Swarm Commands:
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create new image from a container
  cp          Copy files/folders...
  diff...
  events...
  export...
  history...
  import...
  inspect...
  kill...
  load...
  logs...
  pause...
  port...
  rename...
  restart...
  rm...
  rmi...
  save...
  start...
  stats...
  stop...
  top...
  unpause...
  update...
  wait...

Global Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context...
  -D, --debug...
  -H, --host list...
  -l, --log-level...
      --tls...
...
Run 'docker COMMAND --help' for more information.
```

The output confirms that the main commands for managing images and containers are available.

---

## 2. Checking Available Images

The following command was executed:

```bash
docker images
```

Initially, no images were listed:

```text
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

---

## 3. Downloading the Ubuntu Image

The official Ubuntu image was downloaded using:

```bash
docker pull ubuntu
```

The image was downloaded from Docker Hub:

```text
Using default tag: latest
latest: Pulling from library/ubuntu
20043066d3d5: Pull complete
Digest: sha256:c35e29c9450151419d9448b0fd75374fec4fff364a27f176fb458d472dfc9e54
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

The `latest` tag was used by default.

---

## 4. Verifying the Downloaded Image

The following command was executed again:

```bash
docker images
```

The Ubuntu image then appeared in the list:

```text
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ca2b0f26964c   10 days ago   77.9MB
```

The `ubuntu:latest` image was now available locally for creating containers.

---

## 5. Running an Ubuntu Container

The following command was executed:

```bash
docker run ubuntu
```

This command creates and starts a container using the Ubuntu image.

Because no interactive or persistent process was specified, the container exits after its default process finishes.

---

## 6. Creating an Interactive Container

To start an interactive shell, the following command was used:

```bash
docker run --name MeuContainer -it ubuntu bash
```

The container was assigned the following name:

```text
MeuContainer
```

The terminal then displayed:

```text
root@2c6580444ba4:/#
```

From this point onward, commands entered in that terminal were executed inside the Ubuntu container.

---

## 7. Exploring the Container Filesystem

Inside the container, the following command was executed:

```bash
ls
```

The output was:

```text
bin boot dev etc home lib lib32 lib64 libx32 media mnt opt proc root run sbin srv sys tmp usr var
```

This directory structure shows the main directories present in the Ubuntu filesystem inside the container.

---

## 8. Checking the Container Processes

In a second Kali terminal, administrative privileges were obtained:

```bash
sudo -i
```

Next, the following command was executed:

```bash
docker top MeuContainer
```

The output showed the process running inside the container:

```text
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                40370               40342               0                   16:09               pts/0               00:00:00            bash
```

The `docker top` command displays processes associated with a running container.

In this case, the observed main process was `bash`.

---

## 9. Checking Resource Consumption

Still in the second terminal, the following command was executed:

```bash
docker stats
```

The output was:

```text
CONTAINER ID   NAME           CPU %     MEM USAGE / LIMIT   MEM %     NET I/O       BLOCK I/O   PIDS
2c6580444ba4   MeuContainer   0.01%     916KiB / 1.926GiB   0.05%     1.16kB / 0B   0B / 0B     1
```

The `docker stats` command displays resource utilization metrics for running containers.

At the time of the check, `MeuContainer` had the following metrics:

- **CPU usage:** 0.01%
- **Memory usage:** 916 KiB out of 1.926 GiB
- **Memory utilization:** 0.05%
- **PIDs:** 1

---

## 10. Exiting the Container Shell

After completing the checks, the second terminal was closed.

In the first terminal, inside the container, the following command was executed:

```bash
exit
```

The output was:

```text
root@2c6580444ba4:/# exit
exit
```

This closed the interactive shell.

---

## 11. Stopping the Container

The `MeuContainer` container was stopped using:

```bash
docker stop MeuContainer
```

Docker returned:

```text
docker stop MeuContainer
MeuContainer
```

### Evidence — Step 12

**Caption to include before the screenshot:**

> Screenshot of Activity 10.10: execution of the `docker stop MeuContainer` command, confirming that the `MeuContainer` container was stopped.

[View Evidence — Classes 39–40](../evidencias.pdf)

---

## 12. Removing Inactive Containers

After stopping the container, the following command was executed:

```bash
docker container prune
```

Docker requested confirmation:

```text
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```

After confirmation, the stopped containers were removed:

```text
Deleted Containers:
2c6580444ba45dcc6ca52159ef009a52f255b63b612cd2a2075ba0a7c1e5f690
fab9028be5b9edd1614c872ee8cb59877b70e51c1dee2c1f28969a08ea24fd81

Total reclaimed space: 8B
```

The `docker container prune` command removes containers that are no longer running, freeing the resources associated with them.

---

## Key Concepts

- **Docker:** A platform for creating and running containers.
- **Image:** A template used as the basis for creating a container.
- **Container:** A runnable instance of an image.
- **`docker top`:** Displays processes associated with a container.
- **`docker stats`:** Displays resource utilization metrics.
- **`docker stop`:** Stops a running container.

## Activity Workflow

```text
Verify Docker
      ↓
Download the Ubuntu image
      ↓
Create a container
      ↓
Access the shell
      ↓
Check processes
      ↓
Monitor resource usage
      ↓
Exit the container
      ↓
Stop MeuContainer
      ↓
Remove inactive containers
```

## Result

The Ubuntu image was used with Docker to create and run the `MeuContainer` container. Its processes and resource consumption were monitored using `docker top` and `docker stats`, followed by stopping the container and cleaning up inactive containers.

---

[Back to Classes 39–40](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
