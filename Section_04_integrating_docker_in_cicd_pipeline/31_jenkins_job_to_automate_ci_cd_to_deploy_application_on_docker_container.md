# Jenkins Job to automate ci/cd to deploy application on docker container

```
cd /opt/docker; 
docker build -t regapp:v1 .;

# this is horrible idea to do it in this way ^^
docker stop registerapp;
docker rm registerapp;


docker run -d --name registerapp -p 8088:8080 regapp:v1;
```