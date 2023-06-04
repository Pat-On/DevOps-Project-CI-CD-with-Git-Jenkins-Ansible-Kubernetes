# Setup Jenkins Server

- Setup a Linux EC2 Instance
- Install Java
- Install Jenkins
- Start Jenkins
- Access WebUI on port 8080

## SSH client

Open an SSH client.

Locate your private key file. The key used to launch this instance is DevOps_Project_key.pem

Run this command, if necessary, to ensure your key is not publicly viewable.
 chmod 400 DevOps_Project_key.pem

Connect to your instance using its Public DNS:
 ec2-34-253-223-239.eu-west-1.compute.amazonaws.com

ssh -i "DevOps_Project_key.pem" ec2-user@ec2-34-253-223-239.eu-west-1.compute.amazonaws.com

## inside the VM

- sudo su - (root)

### installing Jenkins

- follow `https://pkg.jenkins.io/redhat-stable/`

-` amazon-linux-extras` - it is going to display what other tools I can install using this
- `sudo amazon-linux-extras install java-openjdk11`
- `yum install jenkins`

### checking jenkins status
```
jenkins.service - Jenkins Continuous Integration Server
   Loaded: loaded (/usr/lib/systemd/system/jenkins.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
```

### starting Jenkins service

- `service jenkins start`

