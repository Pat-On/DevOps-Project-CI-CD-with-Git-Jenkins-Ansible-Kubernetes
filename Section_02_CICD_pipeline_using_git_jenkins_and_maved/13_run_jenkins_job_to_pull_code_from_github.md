# Run Jenkins job to pull code from github

- Just create a new item and specify clone code

## Directory in the Jenkins VM
- `Building in workspace /var/lib/jenkins/workspace/


```
[root@jenkins-server PullCodeFromGitHub]# ls -la
total 24
drwxr-xr-x 5 jenkins jenkins  147 Jun  4 15:09 .
drwxr-xr-x 4 jenkins jenkins   53 Jun  4 15:09 ..
-rw-r--r-- 1 jenkins jenkins  130 Jun  4 15:09 Dockerfile
drwxr-xr-x 8 jenkins jenkins  162 Jun  4 15:09 .git
-rw-r--r-- 1 jenkins jenkins 6333 Jun  4 15:09 pom.xml
-rw-r--r-- 1 jenkins jenkins  270 Jun  4 15:09 README.md
-rw-r--r-- 1 jenkins jenkins  479 Jun  4 15:09 regapp-deploy.yml
-rw-r--r-- 1 jenkins jenkins  195 Jun  4 15:09 regapp-service.yml
drwxr-xr-x 3 jenkins jenkins   32 Jun  4 15:09 server
drwxr-xr-x 3 jenkins jenkins   32 Jun  4 15:09 webapp

[root@jenkins-server PullCodeFromGitHub]# pwd
/var/lib/jenkins/workspace/PullCodeFromGitHub
[root@jenkins-server PullCodeFromGitHub]# 

```

```
[root@jenkins-server workspace]# ls
HelloWorldJob  PullCodeFromGitHub
[root@jenkins-server workspace]# pwd
/var/lib/jenkins/workspace
[root@jenkins-server workspace]# 
```