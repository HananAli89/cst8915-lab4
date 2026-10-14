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


### 4. What are the benefits of using Docker Compose over running containers individually?


## Setup Notes

