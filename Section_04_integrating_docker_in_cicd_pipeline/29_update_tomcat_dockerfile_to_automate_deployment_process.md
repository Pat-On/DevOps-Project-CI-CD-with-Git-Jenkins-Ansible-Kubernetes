# Update tomcat dockerfile to automate deplyment process

- We created the docker directory in dockerhost - ./opt/docker
- and gave ownership of it to the dockeradmin
  - `chwon -R dockeradmin:dockeradmin docker`

```
FROM tomcat:latest
RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps
COPY ./*.war /usr/local/tomcat/webapps
~                                         
```
and build the image:
`docker build -t tomcat:v1 .`

```
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
tomcat       v1        b8c9f84a9474   About a minute ago   486MB
```

```
docker run -d --name tomcat:v1 -p 8086:8080 tomcat:v1
```

