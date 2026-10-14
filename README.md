# CST8915 Lab 4: Introduction to Docker

**Student Name**: Hanan Ali

**Student ID**: 041153451

**Course**: CST8915 Full-stack Cloud-native Development

**Semester**: Fall 2026

---

## Demo Video (Part 6: Docker Compose)

🎥 [Watch Demo Video](https://youtu.be/tolYLx2sJdY)

---

## Reflection Questions

### 1. What are the main differences between a Docker image and a Docker container?
An image is a read-only template that holds everything needed to run the app: the base OS, dependencies and code. A container is a running instance of that image. In the lab, I built one image (`my-python-app:v3`) and ran three containers from it (`app1`, `app2`, `app3`). The image stayed the same, while each container ran on its own port and had its own files. You can start, stop and delete containers without changing the image.


### 2. Explain how Docker's layered architecture improves efficiency.
Each instruction in the Dockerfile creates a layer, and Docker caches these layers. When I rebuilt the image without any changes (v2), every step was `CACHED`. When I only changed `app.py` (v3), the `pip install` step was still cached and only the `COPY app.py` step ran again. This makes rebuilds much faster. Layers are also shared, so my containers all used the same 160MB image layers and each one only added about 200kB of its own.


### 3. Why does each container get its own writable layer?
The image layers are read-only so they can be shared safely between containers. Each container gets a thin writable layer on top for any changes it makes. In the lab, I created `data1.txt`, `data2.txt` and `data3.txt` in three containers, and each container could only see its own file. When I modified `app.py` in `app1`, Docker copied it into app1's writable layer first (copy-on-write), so `app2` still had the original. This keeps containers isolated from each other and keeps the image unchanged.


### 4. What are the benefits of using Docker Compose over running containers individually?
With Docker Compose, the whole application is defined in one `docker-compose.yml` file, and one command (`docker compose up -d`) builds the image, pulls Redis, creates the network and volume, and starts both containers. Doing this manually would take several `docker` commands with many options. Compose also puts the services on the same network so the web app can reach Redis just by using the name `redis`. It also makes it easy to manage everything together with `stop`, `start`, `logs` and `down`, and to scale a service with `--scale web=3`.

---

## Setup Notes
- Docker was installed on an Ubuntu 24.04 Azure VM (Standard_B2als_v2 in Sweden Central, since Standard_B2s was not available in my allowed regions).
- I added my user to the `docker` group so I could run Docker commands without `sudo`.
- Before starting Part 6, I removed the containers from Part 5 because one of them was still using port 80, which the Compose `web` service needed.

