# 37 Ansible Playbook to create image and container

```
ll
-rw-rw-r-- 1 ansadmin ansadmin  128 Jun 10 06:38 Dockerfile
-rw-rw-r-- 1 ansadmin ansadmin 2360 Jun 10 06:16 webapp.war
```

## Ansible playbook

- `ansible-playbook`
- `-i` - if not specified inventory default would be used
  - default inventory: /etc/ansible/hosts
    - we can add there ansible IP (private one)

```
[ansadmin@ansible_server docker]$ ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:42ff:fe7e:9737  prefixlen 64  scopeid 0x20<link>
        ether 02:42:42:7e:97:37  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4  bytes 440 (440.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.2.38  netmask 255.255.240.0  broadcast 172.31.15.255
        inet6 fe80::d:72ff:fe93:412f  prefixlen 64  scopeid 0x20<link>
        ether 02:0d:72:93:41:2f  txqueuelen 1000  (Ethernet)
        RX packets 278519  bytes 400915494 (382.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23521  bytes 1864969 (1.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

```
[ansadmin@ansible_server docker]$ cat /etc/ansible/hosts 
[dockerhost]
172.31.20.14

[ansible]           <-- group
172.31.2.38

```


```
[ansadmin@ansible_server docker]$ ansible all -a uptime
The authenticity of host '172.31.2.38 (172.31.2.38)' can't be established.
ECDSA key fingerprint is SHA256:dG6aEV4prn6OZclC/f0RB6XCvccZ2KwVWmzPaoE2H+A.
ECDSA key fingerprint is MD5:0c:ee:6b:4d:2f:b4:45:40:3a:53:45:e9:49:36:ad:a7.
Are you sure you want to continue connecting (yes/no)? [WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
172.31.20.14 | CHANGED | rc=0 >>
 09:43:04 up  4:07,  1 user,  load average: 0.00, 0.00, 0.00
yes 
172.31.2.38 | UNREACHABLE! => {
    "changed": false, 
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '172.31.2.38' (ECDSA) to the list of known hosts.\r\nPermission denied (publickey,gssapi-keyex,gssapi-with-mic,password).", 
    "unreachable": true
}
```

- We need to add ssh key to it

## Copying ssh key to the ansible 

```
[ansadmin@ansible_server docker]$ ssh-copy-id 172.31.2.38 
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansadmin/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansadmin@172.31.2.38's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh '172.31.2.38'"
and check to make sure that only the key(s) you wanted were added.

```

## after all changes all works:
```
[ansadmin@ansible_server docker]$ ansible all -a uptime
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
172.31.20.14 | CHANGED | rc=0 >>
 09:46:56 up  4:11,  1 user,  load average: 0.00, 0.00, 0.00
[WARNING]: Platform linux on host 172.31.2.38 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
172.31.2.38 | CHANGED | rc=0 >>
 09:46:56 up  4:11,  2 users,  load average: 0.00, 0.00, 0.00
```

## creating ansible playbook

- vi regapp.yml

```
[ansadmin@ansible_server docker]$ cat  regapp.yml
---
- hosts: ansible

  tasks: 
  - name: create docker image
    command: docker build -t regapp:latest .
    args: 
      chdir: /opt/docker   
```


```
[ansadmin@ansible_server docker]$ ansible-playbook regapp.yml --check

PLAY [ansible] *******************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************
[WARNING]: Platform linux on host 172.31.2.38 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.31.2.38]

TASK [create docker image] *******************************************************************************************
skipping: [172.31.2.38]

PLAY RECAP ***********************************************************************************************************
172.31.2.38                : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0  
```

```
[ansadmin@ansible_server docker]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
regapp       v1        3aa7a02ee87f   3 hours ago   486MB
tomcat       latest    0fd87ea2d05c   5 days ago    481MB
[ansadmin@ansible_server docker]$ ansible-playbook regapp.yml

PLAY [ansible] *******************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************
[WARNING]: Platform linux on host 172.31.2.38 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.31.2.38]

TASK [create docker image] *******************************************************************************************
changed: [172.31.2.38]

PLAY RECAP ***********************************************************************************************************
172.31.2.38                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

[ansadmin@ansible_server docker]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
regapp       latest    3aa7a02ee87f   3 hours ago   486MB
regapp       v1        3aa7a02ee87f   3 hours ago   486MB
tomcat       latest    0fd87ea2d05c   5 days ago    481MB
```