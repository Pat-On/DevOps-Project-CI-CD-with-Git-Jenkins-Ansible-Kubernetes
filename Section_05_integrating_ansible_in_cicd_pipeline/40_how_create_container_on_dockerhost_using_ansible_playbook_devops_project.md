# How create container on dockerhost using ansible playbook devops project

 ## creating playbook that is going to give instruction to the docker host

 new play book
 ```
 - hosts: dockerhost
  
  tasks:
  - name: create container
    command: docker run -d --name rgapp-server -p 8082:8080 patvon/regapp:latest
```

## checking new playbook
```
[ansadmin@ansible_server docker]$ ansible-playbook deploy_regapp.yml --check

PLAY [dockerhost] ****************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.31.20.14]

TASK [create container] **********************************************************************************************
skipping: [172.31.20.14]

PLAY RECAP ***********************************************************************************************************
172.31.20.14               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0 
```

## first run - problem with pemrission :>
```
[ansadmin@ansible_server docker]$ ansible-playbook deploy_regapp.yml

PLAY [dockerhost] ****************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.31.20.14]

TASK [create container] **********************************************************************************************
fatal: [172.31.20.14]: FAILED! => {"changed": true, "cmd": ["docker", "run", "-d", "--name", "rgapp-server", "-p", "8082:8080", "patvon/regapp:latest"], "delta": "0:00:00.060245", "end": "2023-06-10 11:48:01.648765", "msg": "non-zero return code", "rc": 126, "start": "2023-06-10 11:48:01.588520", "stderr": "docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post \"http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create?name=rgapp-server\": dial unix /var/run/docker.sock: connect: permission denied.\nSee 'docker run --help'.", "stderr_lines": ["docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post \"http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create?name=rgapp-server\": dial unix /var/run/docker.sock: connect: permission denied.", "See 'docker run --help'."], "stdout": "", "stdout_lines": []}

PLAY RECAP ***********************************************************************************************************
172.31.20.14               : ok=1    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   

[ansadmin@ansible_server docker]$ 

```

### Permission problem with /var/run/docker.sock

in the docker server
`/var/run/docker.sock`

`
chmod 777 /var/run/docker.sock

## play book - no issues
```
[ansadmin@ansible_server docker]$ ansible-playbook deploy_regapp.yml

PLAY [dockerhost] ****************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************
[WARNING]: Platform linux on host 172.31.20.14 is using the discovered Python interpreter at /usr/bin/python, but
future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.31.20.14]

TASK [create container] **********************************************************************************************
changed: [172.31.20.14]

PLAY RECAP ***********************************************************************************************************
172.31.20.14               : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

