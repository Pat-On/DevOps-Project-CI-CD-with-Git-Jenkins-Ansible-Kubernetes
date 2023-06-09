# Build a java project using Jenkins

## Create new item 
- Maven Project
- Maven is using pom.xml files as a config files

## Maven Goals and Options
https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

A Build Lifecycle is Made Up of Phases
Each of these build lifecycles is defined by a different list of build phases, wherein a build phase represents a stage in the lifecycle.

For example, the default lifecycle comprises of the following phases (for a complete list of the lifecycle phases, refer to the Lifecycle Reference):

- validate - validate the project is correct and all necessary information is available
- compile - compile the source code of the project
- test - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- package - take the compiled code and package it in its distributable format, such as a JAR.
- verify - run any checks on results of integration tests to ensure quality criteria are met
- install - install the package into the local repository, for use as a dependency in other projects locally
- deploy - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

(There is more of it)

These lifecycle phases (plus the other lifecycle phases not shown here) are executed sequentially to complete the default lifecycle. Given the lifecycle phases above, this means that when the default lifecycle is used, Maven will first validate the project, then will try to compile the sources, run those against the tests, package the binaries (e.g. jar), run integration tests against that package, verify the integration tests, install the verified package to the local repository, then deploy the installed package to a remote repository.



## Where it all was built
```
[INFO] Packaging webapp
[INFO] Assembling webapp [webapp] in [/var/lib/jenkins/workspace/FirstMavenProject/webapp/target/webapp]
[INFO] Processing war project
[INFO] Copying webapp resources [/var/lib/jenkins/workspace/FirstMavenProject/webapp/src/main/webapp]
[INFO] Building war: /var/lib/jenkins/workspace/FirstMavenProject/webapp/target/webapp.war
```

## Where to find the build?

`cd /var/lib/jenkins`

```
[root@jenkins-server jenkins]# ls workspace/
FirstMavenProject  HelloWorldJob  PullCodeFromGitHub
[root@jenkins-server jenkins]# pwd
/var/lib/jenkins
```
