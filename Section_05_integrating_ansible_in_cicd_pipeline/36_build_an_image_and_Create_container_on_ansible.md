# 36 Build an Image and Create Container on Ansible

## Installing docker on the Ansible host

sudo yum install docker -y

- note: this command is going to create as well docker group
- we need to add ansadmin to this group to let him run commands
  - `sudo usermod -aG docker ansadmin`

id ansadmin
```
uid=1001(ansadmin) gid=1001(ansadmin) groups=1001(ansadmin),0(root),992(docker)
```

## getting dockerfile from dockerhost and building image

docker build -t regapp:v1 .