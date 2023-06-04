# Setup a Tomcat Server


Steps:
- setup a linux ec2 instance
- install java
- configure tomcat
- start tomcat server
- access web ui on port 8080



## installing all in the VM
- amazon-linux-extras install java-openjdk11


https://tomcat.apache.org/download-90.cgi

```
[root@ip-172-31-16-113 opt]# pwd
/opt
[root@ip-172-31-16-113 opt]# wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.75/bin/apache-tomcat-9.0.75.tar.gz
```


- tar -xvzf apache-tomcat-9.0.75.tar.gz 


```
[root@ip-172-31-16-113 bin]# ./startup.sh 
Using CATALINA_BASE:   /opt/apache-tomcat-9.0.75
Using CATALINA_HOME:   /opt/apache-tomcat-9.0.75
Using CATALINA_TMPDIR: /opt/apache-tomcat-9.0.75/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /opt/apache-tomcat-9.0.75/bin/bootstrap.jar:/opt/apache-tomcat-9.0.75/bin/tomcat-juli.jar
Using CATALINA_OPTS:   
Tomcat started.
```

```
[root@ip-172-31-16-113 bin]# pwd
/opt/apache-tomcat-9.0.75/bin
```


## You need to modify the configuration of the tomcat server to get access to it from outside - context.xml
```
[root@ip-172-31-16-113 apache-tomcat-9.0.75]# find / -name context.xml
/opt/apache-tomcat-9.0.75/conf/context.xml
/opt/apache-tomcat-9.0.75/webapps/docs/META-INF/context.xml
/opt/apache-tomcat-9.0.75/webapps/examples/META-INF/context.xml
/opt/apache-tomcat-9.0.75/webapps/host-manager/META-INF/context.xml
/opt/apache-tomcat-9.0.75/webapps/manager/META-INF/context.xml
```

```
[root@ip-172-31-16-113 apache-tomcat-9.0.75]# vim /opt/apache-tomcat-9.0.75/webapps/host-manager/META-INF/context.xml
[root@ip-172-31-16-113 apache-tomcat-9.0.75]# vim /opt/apache-tomcat-9.0.75/webapps/manager/META-INF/context.xml
```

## then restart tomcat services

- by script in the bind directory

## update password of tomcat
- in side `conf/tomcat-users.xml`


```xml
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="xxx" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="xxx" roles="manager-script"/>
	<user username="tomcat" password="xxx" roles="manager-gui"/>
```

1. create link files for tomcat startup.sh and shutdown.sh 
   ```sh
   ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
   ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown tomcatup
   ```