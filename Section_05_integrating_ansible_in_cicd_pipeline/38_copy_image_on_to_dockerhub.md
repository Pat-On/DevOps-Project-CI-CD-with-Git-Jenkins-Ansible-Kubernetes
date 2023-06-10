# copy image on to dockerhub

## login to docker

- `docker login`
  - in the real world we would use our own or more likely 3rd party provided for example by AWS

## pushing to docker hub
- add the name of the user a front of the name of the image 
  - `docker tag 3aa7a02ee87f patvon/regapp:latest`

```
REPOSITORY      TAG       IMAGE ID       CREATED       SIZE
regapp          latest    3aa7a02ee87f   4 hours ago   486MB
regapp          v1        3aa7a02ee87f   4 hours ago   486MB
patvon/regapp   latest    3aa7a02ee87f   4 hours ago   486MB
tomcat          latest    0fd87ea2d05c   5 days ago    481MB
```

This will work now:
- `docker push patvon/regapp:latest`
