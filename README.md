# Load Balancer with HAProxy, Docker and Golang Services

## Overview

This project sets up a load balancer using **HAProxy** to distribute traffic between two **Golang services** running in separate **Docker** containers. The services are managed using Docker, and round-robin load balancing is implemented via HAProxy.


## Logs
![Traffic log](https://github.com/priyajha23/Load-balance-haproxy/blob/main/logs/TrafficLog.png)


## Docker Images (Docker Hub Links)

- **Service 1**: (https://hub.docker.com/repository/docker/hahawhytho/21je0702-service1)
- **Service 2**: (https://hub.docker.com/repository/docker/hahawhytho/21je0702-service2)
- **HAProxy**: (https://hub.docker.com/repository/docker/hahawhytho/21je0702-haproxy)

## How to Run  
1. **Pull the images from Docker Hub**:  
   ```sh
   docker pull hahawhytho/21je0702-service1  
   docker pull hahawhytho/21je0702-service2  
   docker pull hahawhytho/21je0702-haproxy  
   ```
2. **Run the containers**:  
   ```sh
   docker run -d --name 21je0702-service1 -p 5001:5000 hahawhytho/21je0702-service1  
   docker run -d --name 21je0702-service2 -p 5002:5000 hahawhytho/21je0702-service2  
   docker run -d --name 21je0702-haproxy -p 80:80 --link 21je0702-service1 --link 21je0702-service2 hahawhytho/21je0702-haproxy  
   ```
3. **Test load balancing**:  
   ```sh
   curl http://localhost  
   ```
4. **Logs of haproxy docker container**
   ```sh
   docker logs 21je0702-haproxy
   ```

---



