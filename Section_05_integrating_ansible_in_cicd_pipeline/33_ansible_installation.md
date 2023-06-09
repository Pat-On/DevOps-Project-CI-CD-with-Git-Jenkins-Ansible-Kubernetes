# Ansible installation

## Prepare Ansible Server
- setup EC2 instance
- setup hostname
- create ansadmin user
- add user to sudoers file
- generate ssh keys
- enable password based login <--- simplification
- install ansible

---

## notes

### creating user admin

useradd ansadmin
passwd ansadmin

visudo
```
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL
ansadmin        ALL=(ALL)       NOPASSWD: ALL
```

### enabling password authentication - simplification of configs - should be token! 

```
vi /etc/ssh/sshd_config
```
```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes
#PermitEmptyPasswords no
#PasswordAuthentication no
```

### Installing Ansible2

```
sudo amazon-linux-extras install ansible2
```