

# Docker Infrastructure

## Introduction

This project demonstrates the creation of a scalable, containerized web application infrastructure using Docker. It includes a reverse proxy, load balancer, front-end static content server, and multiple API servers. Through step-by-step containerization and orchestration, the project showcases how to build, connect, and scale services using Docker and Docker Compose.

---

## Table of Contents

* [Project Structure](#project-structure)
* [Installation](#installation)
* [Usage](#usage)
* [Features](#features)
* [Architecture](#architecture)
* [Configuration](#configuration)
* [Examples](#examples)
* [Troubleshooting](#troubleshooting)
* [Contributors](#contributors)
* [License](#license)

---

## Project Structure

```
holbertonschool-softy-pinko-docker/
├── task0/                  # Base Docker image with Ubuntu
├── task1/                  # Back-end API server with Flask
├── task2/                  # Front-end static content with Nginx
├── task3/                  # Connected front-end and back-end
├── task4/                  # Docker Compose setup
├── task5/                  # Reverse proxy implementation
├── task6/                  # Horizontal scaling of API servers
```

---

## Installation

### Prerequisites

* [Docker Desktop](https://www.docker.com/)
* [Docker Compose](https://docs.docker.com/compose/install/)

> Note: Chromebook users may face compatibility issues; Windows/Mac/Linux are recommended.

### Setup

```bash
# Clone the repository
git clone https://github.com/holbertonschool-softy-pinko-docker.git
cd holbertonschool-softy-pinko-docker
```

---

## Usage

Each task demonstrates a specific step in building the infrastructure:

### Task 0: Build Base Docker Image

```bash
cd task0
docker build -t softy-pinko:task0 .
docker run -it --rm softy-pinko:task0
```

### Task 1: Simple API Server

```bash
cd task1
docker build -t softy-pinko:task1 .
docker run -p 5252:5252 -it --rm softy-pinko:task1
```

### Task 2: Static Front-end Server

```bash
cd task2/front-end
docker build -t softy-pinko-front-end:task2 .
docker run -p 9000:9000 -it --rm softy-pinko-front-end:task2
```

### Task 3: Front-end ↔ Back-end Integration

Ensure CORS is enabled in the back-end and update JavaScript to call API.

### Task 4: Docker Compose Integration

```bash
cd task4
docker-compose build
docker-compose up
```

### Task 5: Add Proxy Server

Update `docker-compose.yml` to include the `proxy` service and route traffic via port `80`.

### Task 6: Horizontal Scaling

```bash
cd task6
docker-compose up --scale back-end=2
```

---

## Features

* 🚀 Containerized back-end and front-end
* 🔁 Round-Robin load balancing
* 🌐 Reverse proxy with Nginx
* 🔌 Full-stack communication via Docker network
* 📈 Horizontal scalability

---

## Architecture

```
               +-------------+
               |   Client    |
               +------+------+
                      |
                      v
            +---------+---------+
            |     Proxy (80)    |
            +----+---------+----+
                 |         |
          +-----------+   +----------------+
          | Front-End |   | Load Balancer  |
          | (Nginx)   |   | (Nginx)        |
          +------+---+    +------+---+----+
                 |                |
         +-------+-----+   +------+------+
         | API Server 1 |   | API Server 2 |
         +-------------+   +-------------+
```

---

## Configuration

* Nginx configuration files:

  * `softy-pinko-front-end.conf` for front-end static server
  * `proxy.conf` for proxy routing rules
* Docker Compose uses internal Docker DNS to resolve service names
* Flask configured to run on `0.0.0.0` for accessibility

---

## Examples

* Front-end loads static content from `/`
* AJAX call to `/api/hello` returns dynamic text from Flask API
* Proxy handles routing transparently to client

---

## Troubleshooting

* Ensure port mappings are correct (`5252`, `9000`, `80`)
* Clear Docker cache if builds behave unexpectedly
* Check container logs for errors:

  ```bash
  docker logs <container_name>
  ```

---

## Contributors

Project by Holberton School students.
Supervised and reviewed by instructional staff.

---

## License

This project is licensed for educational purposes under the Holberton School guidelines.