# Integrate Docker With Jenkins

## Steps:
- Create a dockeradmin user
- install publish over ssh plugin
- add Dockerhost to Jenkins configure systems


## check users on dockerhost
`cat /etc/passwd`


```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
libstoragemgmt:x:999:997:daemon account for libstoragemgmt:/var/run/lsm:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
rngd:x:998:996:Random Number Generator Daemon:/var/lib/rngd:/sbin/nologin
chrony:x:997:995::/var/lib/chrony:/sbin/nologin
ec2-instance-connect:x:996:994::/home/ec2-instance-connect:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
ec2-user:x:1000:1000:EC2 Default User:/home/ec2-user:/bin/bash   <--- our default users
```

To check groups:
`cat ./etc/group`

```
...
dbus:x:81:
ssh_keys:x:998:
rpc:x:32:
libstoragemgmt:x:997:
sshd:x:74:
rpcuser:x:29:
nfsnobody:x:65534:
rngd:x:996:
chrony:x:995:
ec2-instance-connect:x:994:
slocate:x:21:
postdrop:x:90:
postfix:x:89:
stapusr:x:156:
stapsys:x:157:
stapdev:x:158:
screen:x:84:
tcpdump:x:72:
ec2-user:x:1000:
cgred:x:993:
docker:x:992:
```


## Creating user and adding it to use docker group

- `useradd dockeradmin`
- `passwd dockeradmin`

## adding to the group
-`id dockeradmin`
  - `uid=1001(dockeradmin) gid=1001(dockeradmin) groups=1001(dockeradmin)`


- `usermod -aG docker dockeradmin`


## enabling password authentication to ec2

by default ec2 instances does not allow for password authentication
    - we need to enable it

`vi /etc/ssh/sshd_config`

Then you need reload the sshd service

- `service sshd reload`


after this we can easily ssh to our ec2 instance :) 

## Installing `publish over ssh` plugin into jenkins

- simple visual task

