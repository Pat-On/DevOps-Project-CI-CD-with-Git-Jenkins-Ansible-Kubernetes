# Jenkins -> k8s

```
[ansadmin@ansible_server docker]$ cat kube_deploy.yml 
---
#- include: service.yml
#  when: not rabbitmq_docker

#- include: docker.yml
#  when: rabbitmq_docker

- hosts: kubernetes
  # become: true
  user: root

  tasks:
  - name: deploy regapp on kubernetes
    command: kubectl apply -f regapp-deployment.yml
  - name: create service for an app
    command: kubectl apply -f regapp-service.yml
```