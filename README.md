Docker-For-Data-Science 🐳🔬

Welcome to Docker-For-Data-Science, a comprehensive guide to using Docker in your data projects! 🚀

📋 Table of Contents

🚀 Introduction

📦 What are Docker & Containers?

🖼️ Images vs. Containers

🖥️ Docker vs. Virtual Machines

🛠️ Installation

📸 Creating Docker Images

📤 Pushing Images to Docker Hub

🤝 Docker Compose

🚀 Introduction

Docker empowers data scientists to package their workflows—code, libraries, and dependencies—into portable containers that run consistently across any environment. Whether you’re training ML models on your laptop or deploying pipelines in the cloud, Docker ensures reproducibility and scalability in your data projects.

📦 What are Docker & Containers?

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. Docker is the leading platform for building, sharing, and running these containers, providing a CLI and daemon to manage images and containers seamlessly.

🖼️ Images vs. Containers

Docker Image: A read-only template (snapshot) containing instructions (Dockerfile) for creating containers.

Docker Container: A runtime instance of an image; isolated, writable, and encapsulating the environment defined in the image.

Think of an image as a class and a container as an object instantiated from that class. 🏷️➡️📦

🖥️ Docker vs. Virtual Machines

Feature

Virtual Machine

Docker Container

Boot Time

Minutes

Seconds

Resource Overhead

High (full guest OS)

Low (shared host kernel)

Isolation Level

Hardware-level

Process-level

Virtual Machine: Emulates an entire machine (guest OS + virtual hardware) on top of a host system.

Docker Container: Shares the host OS kernel via isolated user-space instances. Lightweight, faster to start, and more resource-efficient.

🛠️ Installation

Follow the official Docker Engine docs to install on Linux, Windows, or macOS. Example for Ubuntu:

# Update package index
sudo apt-get update

# Install prerequisites
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg

# Add Docker’s GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Set up repository & install
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

📸 Creating Docker Images

Write a Dockerfile

FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["python", "train.py"]

Build the image

docker build -t yourusername/ds-project:latest .

Verify

docker images

📤 Pushing Images to Docker Hub

Log in

docker login

Tag (if needed)

docker tag ds-project:latest yourusername/ds-project:latest

Push

docker push yourusername/ds-project:latest

Verify on Docker Hub.

🤝 Docker Compose

Use Docker Compose to define and run multi-container apps via a docker-compose.yml:

version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:7-alpine"

Run it with:

docker compose up --build

Compose handles networks, volumes, and service orchestration in a single YAML file—perfect for data stacks (e.g., Jupyter + Postgres + Redis).

💬 Contributions welcome! Feel free to open issues or submit PRs to improve this guide.
