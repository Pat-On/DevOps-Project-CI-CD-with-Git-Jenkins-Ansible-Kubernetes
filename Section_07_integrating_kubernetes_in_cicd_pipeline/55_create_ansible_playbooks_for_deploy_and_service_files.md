# Ansible Playbook

[ansadmin@ansible_server docker]$ cat kube_deploy.yml 
```
---
- hosts: kubernetes
  <!-- become: true -->
  user: root

  tasks:
  - name: deploy regapp on kubernetes
    command: kubectl apply -f regapp-deployment.yml
```



```
[ansadmin@ansible_server docker]$ cat kube_service.yml 
---
- host: kubernetes
  # become: true
  user: root

  tasks:
  - name: deploy registration app on kubernetes
    command: kubectl apply -f regapp-service.yml
```

## copying our keys to the folder of root users

- `ssh-copy-id root@172.31.7.181`

## manual execution time!

