# Day 31 – Dockerfile: Build Your Own Images

## Task

Today's goal was to write Dockerfiles and build custom Docker images while understanding how Docker images are created and executed.

---

## Task 1: Your First Dockerfile

### Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update && apt-get install -y curl

CMD ["echo","Hello from my custom image!"]
```

### Build Image

```bash
sudo docker build -t my-ubuntu:v1 .
```

### Run Container

```bash
sudo docker run my-ubuntu:v1
```

### Verification

The container successfully printed:

```text
Hello from my custom image!
```

📷 **Screenshot:** `task1-output.png`

---

## Task 2: Dockerfile Instructions

### Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update && apt-get install -y curl

WORKDIR /app

COPY app.txt .

EXPOSE 8080

CMD ["cat","app.txt"]
```

### Understanding Each Instruction

| Instruction | Description                                    |
| ----------- | ---------------------------------------------- |
| `FROM`      | Uses Ubuntu as the base image.                 |
| `RUN`       | Executes commands during image build.          |
| `WORKDIR`   | Sets `/app` as the working directory.          |
| `COPY`      | Copies `app.txt` from the host into the image. |
| `EXPOSE`    | Documents that the application uses port 8080. |
| `CMD`       | Runs `cat app.txt` when the container starts.  |

### Build

```bash
sudo docker build -t docker-demo:v1 .
```

### Run

```bash
sudo docker run docker-demo:v1
```

📷 **Screenshot:** `task2-output.png`

---

## Task 3: CMD vs ENTRYPOINT

### CMD

```dockerfile
FROM ubuntu

CMD ["echo","hello"]
```

Running:

```bash
sudo docker run cmd-demo:v1
```

Output:

```text
hello
```

Running:

```bash
sudo docker run cmd-demo:v1 ls
```

Docker ignored the default `CMD` and executed `ls` instead.

### ENTRYPOINT

```dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]
```

Running:

```bash
sudo docker run entry-demo:v1 hello
```

Output:

```text
hello
```

Running:

```bash
sudo docker run entry-demo:v1 Docker Rocks!
```

Output:

```text
Docker Rocks!
```

### When would you use CMD vs ENTRYPOINT?

* **CMD** is used when you want to provide a default command that users can override.
* **ENTRYPOINT** is used when the container should always run the same executable, while allowing additional arguments to be passed.

---

## Task 4: Build a Simple Web App Image

### index.html

A simple static HTML page.

### Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/

EXPOSE 80
```

### Build

```bash
sudo docker build -t my-website:v1 .
```

### Run

```bash
sudo docker run -d -p 8080:80 my-website:v1
```

### Port Mapping

* **8080** → Host (EC2) port
```text
http://<EC2-Public-IP>:8080


---

## Task 5: .dockerignore


```text
.git
*.md
.env
```

### Observation


---
## Task 6: Build Optimization

### Observation

Docker reused cached image layers during rebuilds when no changes were made.

### Why does layer order matter?


---

## Key Takeaways

* Built custom Docker images using Dockerfiles.
* Learned the purpose of common Dockerfile instructions.
* Understood the difference between `CMD` and `ENTRYPOINT`.
* Built and deployed a static website using Nginx.
* Used `.dockerignore` to optimize the build context.
* Learned how Docker layer caching speeds up image builds.
Docker builds images layer by layer. If a layer has not changed, Docker reuses the cached version instead of rebuilding it. Placing frequently changing instructions near the end of the Dockerfile improves build performance because only the modified layers need to be rebuilt.

The `.dockerignore` file excludes unnecessary files from the Docker build context, reducing build time, keeping images smaller, and preventing sensitive files from being copied into the image.
node_modules
### .dockerignore
📷 **Screenshot:** `task4-output.png`
```

The website was successfully accessed in the browser using:
* **80** → Container (Nginx) port

