# Load Balancer with HAProxy and Golang Services

## Overview

This project sets up a load balancer using **HAProxy** to distribute traffic between two **Golang services** running in separate Docker containers. The services are managed using Docker, and round-robin load balancing is implemented via HAProxy.

## How to Run  
1. **Build and Run Service 1**:  
   ```sh
   cd service1
   docker build -t service1 .
   docker run -d --name service1 -p 5001:5000 service1
   ```

2. **Build and Run Service 1**:
    ```sh 
    cd ../service2
    docker build -t service2 .
    docker run -d --name service2 -p 5002:5000 service2
    ```
   
3. **Build and Run HAProxy**:  
   ```sh
   cd ../haproxy
   docker build -t haproxy .
   docker run -d --name haproxy -p 80:80 --link service1 --link service2 haproxy
   ```
4. **Run the containers**:  
   ```sh
   docker run -d --name service1 -p 5001:5000 <your-dockerhub-username>/service1  
   docker run -d --name service2 -p 5002:5000 <your-dockerhub-username>/service2  
   docker run -d --name haproxy -p 80:80 --link service1 --link service2 <your-dockerhub-username>/haproxy  
   ```
5. **Test load balancing**:  
   ```sh
   curl http://localhost  
   ```
6. **Load Balancing Verification**:  
    ```sh
     docker logs haproxy
     ```
7. **Stopping and Cleaning Up**:  
    ```sh
    docker stop haproxy service1 service2
    docker rm haproxy service1 service2
    docker rmi haproxy service1 service2  # Remove images if needed
    ```




## Docker Images (Docker Hub Links)

- **Service 1**: [service1](https://hub.docker.com/repository/docker/hahawhytho/21je0702-service1)
- **Service 2**: [service2](https://hub.docker.com/repository/docker/hahawhytho/21je0702-service2)
- **HAProxy**: [haproxy](https://hub.docker.com/repository/docker/hahawhytho/21je0702-haproxy)



---



