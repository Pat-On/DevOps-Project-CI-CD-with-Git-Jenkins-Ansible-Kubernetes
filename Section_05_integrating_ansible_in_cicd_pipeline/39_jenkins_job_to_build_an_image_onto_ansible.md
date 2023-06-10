# Jenkins job to build an image onto ansible

## adding two additional tasks to the playbook

```
- hosts: ansible

  tasks:
  - name: create docker image
    command: docker build -t regapp:latest .
    args:
      chdir: /opt/docker
        
  - name: create tag to push image onto dockerhub
    command: docker tag regapp:latest patvon/regapp:latest
      
  - name: push docker image
    command: docker push patvon/regapp:latest
```

ansible-playbook regapp.yml --check

validation:
- `ansible-playbook regapp.yml --check`

## limiting server
- ansible-playbook regapp.yml --limit localhost


## then you need to add this command into the Jenkins server 
 
 `ansible-playbook /opt/docker/regapp.yml`