# Integrate Maven with Jenskins

- we will instal maven on Jenkins server to reduce the complexity


- setup Maven on Jenkins Server
- setup environment variables
  - JAVA_HOME
  - M2
  - M2_HOME
- Install MAven Plugin
- Configure Maven and Java


## Official documentation
https://maven.apache.org/install.html


https://maven.apache.org/download.cgi
https://dlcdn.apache.org/maven/maven-3/3.9.2/binaries/apache-maven-3.9.2-bin.tar.gz

## In the linux machine

- go to `./opt` directory

- wget https://dlcdn.apache.org/maven/maven-3/3.9.2/binaries/apache-maven-3.9.2-bin.tar.gz

- tar -xvzf apache-maven-3.9.2-bin.tar.gz 

## setting environment variables for Maven


```
M2_HOME=/opt/maven
M2=/opt/maven/bin
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.19.0.7-1.amzn2.0.1.x86_64


# User specific environment and startup programs

PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2

```

#### To find Java Installation
```
find / -name jvm

find / -name java-11*
```


#### to load changes you can:
- `source .bash_profile`



## then instal plugin and point where Maven and Java is installed

