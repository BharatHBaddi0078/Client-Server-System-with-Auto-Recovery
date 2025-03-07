# Synchronized Client-Server Communication System

## Overview
This project implements a synchronized client-server model using Python sockets. Clients send numbers alternately to the server in a turn-based fashion. The system is containerized using Docker and deployable on Kubernetes.

## Features
- **Turn-based communication** between clients and the server.
- **Automatic recovery**: Clients attempt to reconnect if disconnected.
- **Containerized with Docker** for portability.
- **Kubernetes deployment** for scalability and fault tolerance.

## Project Structure
```
├── Dockerfile.client           # Dockerfile for client
├── Dockerfile.server           # Dockerfile for server
├── README.md                   # Project documentation
├── client-deployment.yaml      # Kubernetes deployment for clients
├── client.py                   # Client script
├── server-deployment.yaml      # Kubernetes deployment for server
├── server.py                   # Server script
```

## How It Works
1. **Server (`server.py`)**:
   - Manages turn-based communication.
   - Listens for two clients and ensures orderly message exchange.

2. **Client (`client.py`)**:
   - Two clients run in separate threads, sending numbers alternately.
   - Clients wait for a "GO" signal from the server before sending data.

## Installation & Usage
### Running Locally
1. **Start the server**:
   ```bash
   python3 server.py
   ```
2. **Start the clients**:
   ```bash
   python3 client.py
   ```

### Running with Docker
1. **Build and run the server**:
   ```bash
   docker build -t server-image -f Dockerfile.server .
   docker run -p 5000:5000 server-image
   ```
2. **Build and run the client**:
   ```bash
   docker build -t client-image -f Dockerfile.client .
   docker run client-image
   ```

### Running with Kubernetes
1. **Apply the manifests**:
   ```bash
   kubectl apply -f server-deployment.yaml
   kubectl apply -f client-deployment.yaml
   ```
2. **Check running pods**:
   ```bash
   kubectl get pods
   ```

## Technologies Used
- **Python** (Sockets, Multithreading)
- **Docker** (Containerization)
- **Kubernetes** (Deployment and Scalability)

## Expected Output
- The server receives numbers in an alternating sequence from two clients.
- Clients send numbers only when permitted by the server.
- The system recovers from failures automatically.

## Troubleshooting
- **Address already in use:** Stop any existing process using port `5000`:
  ```bash
  sudo lsof -i :5000
  sudo kill -9 <PID>
  ```
- **Connection refused:** Ensure the server is running before starting clients.
- **Check Kubernetes logs:**
  ```bash
  kubectl logs <pod-name>
  ```


