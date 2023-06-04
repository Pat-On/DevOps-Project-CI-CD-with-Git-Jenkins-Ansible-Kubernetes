# Run 1st Jenkins Job

## Inside Jenkins
- We can easily create a new job but unfortunately most of the features of jenkins coming with a plugins, so we need to install them :>

### HelloWorld Jenkins job

Selected cli: bash, because used system is linux
executed commands:
- echo "Hello World"
- uptime

```
Started by user admin
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/HelloWorldJob
[HelloWorldJob] $ /bin/sh -xe /tmp/jenkins6949372472365720913.sh
+ echo 'Hello World'
Hello World
+ uptime
 12:25:38 up 27 min,  1 user,  load average: 0.03, 0.10, 0.08
Finished: SUCCESS
```