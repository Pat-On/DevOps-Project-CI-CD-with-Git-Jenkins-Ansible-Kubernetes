# Continuous deployment of docker container using ansible playbook

Steps:
- remove existing container
- remove existing image
- create new container

[totally not production like solution ^^]

## updating ansible playbook

```
- hosts: dockerhost

  tasks:
  - name: stop existing container
    command: docker stop regapp-server

  - name: remove the container
    command: docker rm regapp-server

  - name: remove image
    command: docker image rm patvon/regapp:latest

  - name: create container
    command: docker run -d --name rgapp-server -p 8082:8080 patvon/regapp:latest

```

## error handling:

```
- hosts: dockerhost

  tasks:
  - name: stop existing container
    command: docker stop regapp-server
    ignore_errors: yes

  - name: remove the container
    command: docker rm regapp-server
    ignore_errors: yes

  - name: remove image
    command: docker image rm patvon/regapp:latest
    ignore_errors: yes

  - name: create container
    command: docker run -d --name regapp-server -p 8082:8080 patvon/regapp:latest
```