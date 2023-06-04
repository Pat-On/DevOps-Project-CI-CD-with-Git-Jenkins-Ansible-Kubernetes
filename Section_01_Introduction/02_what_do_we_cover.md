# What do we cover

- we will deploy app to three different environments:
  - vm
  - docker container
  - k8s cluster


## Build and Deploy on Tomcat Server
- setup ci/cd with github jenkins maven and tomcat
  - setup jenkins
  - setup and configure maven and git
  - setup tomcat server
  - integrating github, maven tomcat server with jenkins
  - create a CI and CD jobs
  - test the deployment

## Deploy artifacts on a container
- setup ci cd with github jenkins maven and docker
  - setting up docker env
  - write dockerfile
  - create an IMimage and container on docker host
  - integrate docker host with jenkins
  - create ci cd job on jenkins to build and deploy on a container

## Deploy artifacts on a container
- ci/cd with github, jenkins, maven, ansible and docker
  - setup ansible server
  - integrate docker host with ansible
  - ansible playbook to create image
  - ansible playbook to create continuer
  - integrate ansible with jenkins
  - ci/cd job to build code on ansible and deploy it on docker container

## Deploy Artifacts on Kubernetes
- ci/cd with github, jenkins, maven, ansible and k8s
  - setup EKS
  - write pod, service and deployment manifest files
  - integrate k8s with ansible
  - ansible playbooks to create deployment and service
  - ci/cd job to build code on ansible and deploy it on k8s
  - 