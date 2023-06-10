# Integrate ansible with Jenkins

note: we are going to use jenkins to copy artifact and ansible is going to build docker image and deploy it to the docker host

manage jenkins - >system -> publish over ssh

## Creating the new new item in the Jenkins

- remember to always change the owner of the directory - permission issue
  - solution: `sudo chown ansadmin:ansadmin docker`

