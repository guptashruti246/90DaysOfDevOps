# Day 30 - Docker Images & Container Lifecycle

## Task 1: Docker Images

### Pull Images

```bash
sudo docker pull nginx
sudo docker pull ubuntu
sudo docker pull alpine
```

### List Images

```bash
sudo docker images
```

### Observation

* `alpine` is significantly smaller because it is a minimal Linux distribution designed specifically for containers.
* `ubuntu` contains many additional packages and utilities, making it larger.
* `nginx` includes the web server binaries and dependencies.

### Inspect an Image

```bash
sudo docker inspect nginx
```

### Remove Images

```bash
sudo docker rmi alpine:latest
sudo docker rmi nginx:latest
sudo docker rmi ubuntu:latest
```

Docker prevented deletion of the Ubuntu image because it was associated with a stopped container.

Remove the stopped container first:

```bash
sudo docker rm fcbbef417d93
sudo docker rmi ubuntu:latest
```

---

## Task 2: Image Layers

### View Image History

```bash
sudo docker image history nginx
```

### Observation

Docker images are built using layers. Each layer represents a change made to the image, such as installing packages or copying files.

Benefits of layers:

* Faster image builds
* Layer caching
* Reduced storage consumption
* Efficient image sharing

---

## Task 3: Container Lifecycle

### Create a Container

```bash
sudo docker create ubuntu
```

### Start Container

```bash
sudo docker start <container_id>
```

### Pause Container

```bash
sudo docker pause <container_id>
```

### Unpause Container

```bash
sudo docker unpause <container_id>
```

### Stop Container

```bash
sudo docker stop <container_id>
```

### Restart Container

```bash
sudo docker restart <container_id>
```

### Kill Container

```bash
sudo docker kill <container_id>
```

### Remove Container

```bash
sudo docker rm <container_id>
```

### Check Container States

sudo docker ps -a
```


> Note: Screenshots for Task 3 were intentionally skipped. The commands were executed and observed during practice.


---

## Task 4: Working with Running Containers


### Run Nginx Container

```bash
sudo docker run -d nginx
```


### View Logs

```bash
sudo docker logs <container_id>

```


### Follow Logs in Real Time

```bash
sudo docker logs -f <container_id>
```

Press `Ctrl + C` to exit.

### Enter Container


```bash
sudo docker exec -it <container_id> sh
```

### Run a Single Command Inside Container

```bash
sudo docker exec <container_id> ls /usr/share/nginx/html
```

### Inspect Container

```bash
sudo docker inspect <container_id>
```

### Get Container IP Address

```bash
sudo docker inspect -f '{{.NetworkSettings.IPAddress}}' <container_id>
```

### Check Port Mapping

```bash
sudo docker port <container_id>
```

No output was displayed because the container was started without publishing any ports.

### Check Mounts

```bash
sudo docker inspect -f '{{json .Mounts}}' <container_id>
```

---

## Task 5: Cleanup

### Stop All Running Containers

```bash
sudo docker stop $(sudo docker ps -q)
```

### Remove All Stopped Containers

```bash
sudo docker container prune -f
```

### Remove Unused Resources

```bash
sudo docker system prune -a
```

### Check Docker Disk Usage

```bash
sudo docker system df
```

---

## Screenshots

### SS1 – Docker Images

![Docker Images](screenshots/docker-images.png)

---

### SS2 – Nginx Image History

![Image History](screenshots/nginx-image-history.png)

---

### SS3 – Container Logs

![Container Logs](screenshots/nginx-running.png)

---

### SS4 – Docker Disk Usage

![Docker System DF](screenshots/docker-disk-usgae.png)

---

## Key Learnings

* Docker images are immutable templates.
* Containers are running instances of images.
* Docker layers enable efficient storage and caching.
* Containers transition through different states during their lifecycle.
* Docker provides commands to inspect, monitor, and clean up resources efficiently.


