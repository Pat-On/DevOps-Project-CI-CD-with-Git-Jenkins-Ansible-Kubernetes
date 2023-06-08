# create a (not) first docker in ci/cd pipeline :>

- `FROM` - to pull the based image
- `RUN` - to execute commands
- `CMD` - to provide defaults for an executing container (can be overwritten)
- `ENTRYPOINT` to configure a container that will run as an executable (can not be overwritten)
- `WORKDIR` to sets the working directory
- `COPY` to copy a directory from your local machine to the docker container
- `ADD` to copy files and folders from you local machine to docker container
- `EXPOSE` informs docker that the containers listens on the specified network ports at runtime
- `ENV` to set env variables

## Steps
- Pull centos from dockerhub                    `FROM`
- install java                                  `RUN`
- create /opt/tomcat directory                  `RUN`
- change work directory to /opt/tomcat          `WORKDIR`
- download tomcat packages                      `ADD/RUN`
- extract tar.gz file                           `RUN` - TAR COMMAND
- rename to tomcat directory                    `RUN`
- tell to docker that it runs on port 8080      `EXPOSE`
- start tomcat services                         `CMD` - because this will be executed at the docker tun time

Bugged
```
FROM centos
RUN yum install java -y
RUN mkdir /opt/tomcat/
WORKDIR /opt/tomcat
ADD https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz /opt/tomcat
RUN tar xvfz apache*.tar.gz
RUN mv apache-tomcat-9.0.54/* /opt/tomcat 
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
```

```
FROM centos:7
RUN yum install java -y
RUN mkdir /opt/tomcat/
WORKDIR /opt/tomcat
ADD https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.75/bin/apache-tomcat-9.0.75.tar.gz /opt/tomcat
RUN tar xvfz apache*.tar.gz
RUN mv apache-tomcat-9.0.75/* /opt/tomcat 
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
```

to make it working with a newest
```
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-* &&\ 
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Linux-*
```