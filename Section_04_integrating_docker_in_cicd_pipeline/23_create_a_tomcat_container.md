# 23 Create a tomcat container


```
            Docker Hub  |(docker pull)
                        V
Dockerfile  -----> Docker Image  ---------------------> Docker Container
            (docker build)          (docker run)

```

DockerHub! again :>

## https://hub.docker.com/_/tomcat

`docker run -d --name tomcat-container -p 8081:8080 tomcat` 

## How we exposed ports

- docker container 8081:8080
- security group:
  - open port from 8081-9000 from 0.0.0.0/0