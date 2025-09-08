# Holberton Softy Pinko Docker

This project explores **application containerization** with Docker and Docker Compose, implementing a modern infrastructure with a **reverse proxy**, **load balancer**, API servers, and a static content server.

---

## 📌 Context

Docker allows you to package applications into portable, self-contained environments that can run anywhere. This project demonstrates how to:
- Create Docker images for different services.
- Use Docker Compose to orchestrate multiple containers.
- Set up a **reverse proxy** and **load balancer** with Nginx.
- Scale services horizontally to handle traffic.

---

## 📂 Project Structure

holbertonschool-softy-pinko-docker/ 

├──task0/          # First Docker container (Ubuntu + "Hello, World!") 

├── task1/          # Flask API server 

├── task2/          # Static front-end server with Nginx 

├── task3/          # Front-end/back-end connection with CORS 

├── task4/          # Orchestration with Docker Compose 

├── task5/          # Reverse proxy setup 

├── task6/          # Load balancing with multiple API servers 

└── README.md

---

## 🚀 Tasks Completed

### **Task 0: First Docker Container**
- **Goal**: Create a Docker image based on Ubuntu that prints "Hello, World!".
- **Files**:
  - `Dockerfile`: Installs updates and prints a message.
- **Commands**:
  ```bash
  docker build -t softy-pinko\:task0 .
  docker run -it --rm softy-pinko\:task0

### **Task 1: Back-end Flask Server**

- **Goal**: Create a Flask API server with a `/api/hello` endpoint.

- **Files**:

  - `Dockerfile`: Installs Python3, pip3, and Flask.
  - `api.py`: Flask code for the endpoint.

- **Commands**:

  ```bash
  docker build -t softy-pinko\:task1 .
  docker run -p 5252:5252 -it --rm softy-pinko\:task1
  
  ```

- **Access**: `http://localhost:5252/api/hello`



------

### **Task 2: Static Front-end Server**

- **Goal**: Serve a static webpage using Nginx.

- **Files**:

  - `Dockerfile`: Uses the Nginx image.
  - `softy-pinko-front-end.conf`: Nginx configuration (port 9000).

- **Commands**:

  ```
   Copierdocker build -t softy-pinko-front-end\:task2 ./front-end
  docker run -p 9000:9000 -it --rm softy-pinko-front-end\:task2
  ```

- **Access**: `http://localhost:9000`

------

### **Task 3: Connect Front-end and Back-end**

- **Goal**: Enable communication between front-end and back-end using AJAX.

- **Changes**:

  - Added `<h1 id="dynamic-content"></h1>` to `index.html`.
  - jQuery script to call `/api/hello`.
  - Installed `flask-cors` to allow cross-origin requests.

- **Commands**:

  ```bash
  docker build -t softy-pinko-back-end\:task3 ./back-end
  docker build -t softy-pinko-front-end\:task3 ./front-end
  docker run -p 5252:5252 softy-pinko-back-end\:task3
  docker run -p 9000:9000 softy-pinko-front-end\:task3
  
  ```



### **Task 4: Docker Compose Orchestration**

- **Goal**: Simplify container management with `docker-compose.yml`.

- **Files**:

  - `docker-compose.yml`: Defines `back-end` and `front-end` services.

- **Commands**:

  ```bash
  docker compose build
  docker compose up
  ```

------

### **Task 5: Reverse Proxy with Nginx**

- **Goal**: Centralize requests through an Nginx reverse proxy.

- **Files**:

  - `proxy/Dockerfile`: Nginx image for the proxy.
  - `proxy/proxy.conf`: Routes `/` to front-end and `/api/` to back-end.
  - Updated JavaScript to call `/api/hello` (via proxy).

- **Commands**:

  ```bash
  docker compose up
  ```

- **Access**: `http://localhost` (all traffic goes through the proxy).

------

### **Task 6: Load Balancing**

- **Goal**: Scale the back-end to 2 instances and load balance requests.

- **Files**:

  - `2-api-servers.txt`: Contains the command `docker compose up --scale back-end=2`.

- **Commands**:

  ```bash
   docker compose up --scale back-end=2
  ```

- **Result**: Requests to `/api/hello` are distributed between 2 API servers (Round-Robin).

------

## 🛠 Technologies Used

| Tool               | Role                              |
| ------------------ | --------------------------------- |
| **Docker**         | Containerize applications.        |
| **Docker Compose** | Orchestrate containers.           |
| **Nginx**          | Reverse proxy and load balancer.  |
| **Flask**          | Python API server.                |
| **jQuery**         | AJAX requests from the front-end. |



------

## 📦 Prerequisites

- [Docker Desktop](https://www.docker.com/) installed.
- Basic knowledge of Docker and Docker Compose.

------

## 🎯 Key Features

1. **Service Isolation**: Each component (front-end, back-end, proxy) runs in its own container.
2. **Reverse Proxy**: Nginx routes requests to the correct service.
3. **Load Balancing**: Automatically distributes requests between multiple back-end instances.
4. **Portability**: The application can be deployed anywhere with Docker.

------

## 📚 Useful Resources

- [Docker Cheatsheet](https://dockerlabs.collabnix.com/docker/cheatsheet/)
- [Proxy vs Reverse Proxy](https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/)
- [Round Robin Load Balancing](https://www.nginx.com/resources/glossary/round-robin-load-balancing/)

------

## 📝 Author

**Anne-Cécile Colléter**