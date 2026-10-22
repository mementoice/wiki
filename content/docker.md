---
title: Docker
tags:
  - tools/containers
---

# Docker

```text
- Docker packages an app and its dependencies into a portable image.
- An image is a frozen package; a container is a running copy of it.
- Containers share the host kernel, so they are light and start quickly.
- Sharing the kernel makes container isolation weaker than a VM's.
- Data written inside a container is temporary; a volume keeps it.
```

Docker builds, ships, and runs applications in **containers**. A container packages an app with its dependencies and runs it as an isolated process.

## The vital few

Most Docker work uses five ideas:

1. **Image** — a read-only package with the app, runtime, libraries, and config.
2. **Container** — a running instance of an image.
3. **Dockerfile** — a text recipe for building an image.
4. **Registry** — a store for images. Docker Hub is the default public registry.
5. **Volume** — persistent storage outside the container's writable layer.

Learn these five, and you can use most of Docker. Networks, Compose, and orchestration add convenience or scale.

## Analogy: shipping containers

A shipping container is a standard box. Any crane and ship can move it. The contents do not change when the box moves.

A Docker image is the box. A container is the box in use. A registry is the port where boxes are stored.

Where the analogy breaks: software containers are not fully separate machines. They share the host kernel. This makes them light, but it also makes their isolation weaker than a virtual machine's.

## How it works

A container is a Linux process with three changes:

1. **Namespaces** give it its own view of the system: process IDs, network, mounts, and hostname.
2. **cgroups** limit and measure its CPU, memory, and I/O.
3. **A layered filesystem** gives it an image-based root filesystem. Image layers are read-only; the container adds a thin writable layer.

Docker assembles these pieces. On Linux, the Docker daemon (`dockerd`) talks to containerd, which starts containers with a runtime such as runc. On macOS and Windows, Docker Desktop runs a small Linux VM, because Linux containers need a Linux kernel.

## Image vs container

An image is the recipe and the frozen files. A container is a running copy of that image. You can start many containers from one image. Changes inside a container do not change the image.

Images are immutable and built from layers. Each Dockerfile instruction adds a layer. Docker caches layers, so a rebuild can reuse unchanged steps.

## Docker vs virtual machine

|                   | Container                             | Virtual machine                    |
| ----------------- | ------------------------------------- | ---------------------------------- |
| Isolation         | Process-level; shares the host kernel | Hardware-level; has its own kernel |
| Size              | Often megabytes                       | Often gigabytes                    |
| Start time        | Milliseconds to seconds               | Seconds to minutes                 |
| Density           | High; many per host                   | Lower                              |
| Security boundary | Weaker                                | Stronger                           |
| Use when          | Packaging and shipping apps           | Strong isolation or a different OS |

Containers are not a strong security boundary for untrusted code. Use a VM or a sandbox when the workload is hostile.

## Worked example: a Python app

A minimal `Dockerfile`:

```dockerfile
FROM python:3.13-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["python", "app.py"]
```

Build and run it:

```bash
docker build -t myapp .
docker run -d --name myapp -p 8000:8000 myapp
docker ps
docker logs myapp
docker stop myapp
```

What happens:

- `docker build` reads the Dockerfile and creates the image `myapp`.
- `docker run` starts a container from that image.
- `-p 8000:8000` maps host port 8000 to container port 8000.
- `-d` runs the container in the background.
- `docker logs` shows its output.

To keep data after the container is removed, use a volume:

```bash
docker run -d --name myapp -p 8000:8000 -v mydata:/data myapp
```

## Compose

Compose defines a multi-container app in one YAML file:

```yaml
services:
  web:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - ./data:/data
```

Start it with `docker compose up --build`. Compose is common for local development.

## Common mistakes

- **Storing data in the container.** The writable layer disappears with the container. Use a volume.
- **Baking secrets into the image.** Anyone with the image can read them. Inject secrets at run time.
- **Running as root.** Add a `USER` instruction and use a non-root account.
- **Using `latest` in production.** Pin a version tag or a digest.
- **Sending a huge build context.** Add a `.dockerignore` file.
- **Treating containers as a security sandbox.** Use a VM or a dedicated sandbox for untrusted code.

## Sources

- [Docker: What is an image?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/)
- [Docker: What is a registry?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry/)
- [Docker: Dockerfile concepts](https://docs.docker.com/build/concepts/dockerfile/)
- [Docker: dockerd reference](https://docs.docker.com/reference/cli/dockerd)
- [containerd: Runtime v2](https://containerd.io/docs/main/runtime-v2/)
- [Microsoft: Containers vs. virtual machines](https://learn.microsoft.com/en-us/virtualization/windowscontainers/about/containers-vs-vm)
