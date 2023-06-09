# Integrate Docker With Ansible

## Manage DockerHost with Ansible

- on docker host
  - create ansadmin
  - add ansadmin to sudoers files
  - enable password based login

- on ansible node
  - add to hosts file
  - copy ssh keys from ansible
  - test the connection

### Docker host

useradd ansadmin
passwd ansadmin

edit visudo password requirements to run commands and auth

enabling password authentication - already done
- confirmation `grep Password /etc/ssh/sshd_config`

### Ansible Server

vi /etc/ansible/hosts
- adding private address of the docker to it
  
copying the ssh key via this command:

```
[ansadmin@ip-172-31-2-38 ~]$ ssh-copy-id 172.31.20.14
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansadmin/.ssh/id_rsa.pub"
The authenticity of host '172.31.20.14 (172.31.20.14)' can't be established.
ECDSA key fingerprint is SHA256:NSysHzfX1x3mRTFevYzLSsXglkXlgIyim+qKR683gG4.
ECDSA key fingerprint is MD5:59:aa:b5:4d:49:4f:1b:e3:ba:08:71:cf:9e:34:0f:85.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansadmin@172.31.20.14's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh '172.31.20.14'"
and check to make sure that only the key(s) you wanted were added.

[ansadmin@ip-172-31-2-38 ~]$ 
```

### Validating connection
```
[ansadmin@ip-172-31-2-38 ~]$ ansible all -m ping
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
172.31.20.14 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
```



```
[ansadmin@ip-172-31-2-38 ~]$ ansible all -m command -a uptime
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
172.31.20.14 | CHANGED | rc=0 >>~
 05:47:01 up  1:14,  3 users,  load average: 0.00, 0.00, 0.00
```