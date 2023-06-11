# Integrating Kubernetes Bootstrap Server with Ansible

## Steps

- On Bootstrap server
  - Create ansadmin
  - add ansadmin to sudoers files

- On Ansible Node
  - Add to hosts file
  - Copy ssh keys
  - Test the connection

Ansible ------- > Kubernetes

- useradd ansadmin
- visudo

```
## Allow root to run any commands anywhere 
root    ALL=(ALL)       ALL
ansadmin  ALL=(ALL)  NOPASSWD: ALL

```

## enabling password based authentication for sake of simplicity
- vi /etc/ssh/sshd_config

```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes
#PermitEmptyPasswords no
#PasswordAuthentication no

```

service sshd reload

## Creating hosts file
```
[ansadmin@ansible_server docker]$ cat hosts 
localhost

[kubernetes]
172.31.7.181

[ansible]
172.31.2.38
```


## copying ssh
ssh-copy-id 172.31.7.181


## to verify
- `ansible -i hosts  all -a uptime`

