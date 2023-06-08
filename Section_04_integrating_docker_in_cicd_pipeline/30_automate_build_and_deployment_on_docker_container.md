# Automate Build and Deployment on Docker Container

## Adding Exec command to SSH Publishers

```
cd /opt/docker; 
docker build -t regapp:v1 .; builds
docker run -d --name registerapp -p 8088:8080 regapp:v1; <-- it will be the reason of errors in future container name
```

this was such a simple step after this all pre-configured systems