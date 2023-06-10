# Jenkins CI/CD to deploy on container using ansible

## Automating it! 

inside the items in the Jenskins we are going to add one more ansible-playbook command:

```
ansible-playbook /opt/docker/regapp.yml;
sleep 10;
ansible-playbook  /opt/docker/deploy_regapp.yml;
```