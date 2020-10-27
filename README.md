# spring-boot-buildpack

[![Build Status](https://travis-ci.com/jonashackt/spring-boot-buildpack.svg?branch=main)](https://travis-ci.com/jonashackt/spring-boot-buildpack)
[![License](http://img.shields.io/:license-mit-blue.svg)](https://github.com/jonashackt/spring-boot-buildpack/blob/master/LICENSE)
[![renovateenabled](https://img.shields.io/badge/renovate-enabled-yellow)](https://renovatebot.com)
[![versionspringboot](https://img.shields.io/badge/dynamic/xml?color=brightgreen&url=https://raw.githubusercontent.com/jonashackt/spring-boot-buildpack/master/pom.xml&query=%2F%2A%5Blocal-name%28%29%3D%27project%27%5D%2F%2A%5Blocal-name%28%29%3D%27parent%27%5D%2F%2A%5Blocal-name%28%29%3D%27version%27%5D&label=springboot)](https://github.com/spring-projects/spring-boot)

Example project showing how to use Buildpacks.io together with Spring Boot &amp; it's layered jar feature


### Buildpacks?

* Heroku invented (2011)

> Buildpacks were first conceived by Heroku in 2011. Since then, they have been adopted by Cloud Foundry (Pivotal) and other PaaS such as Google App Engine, Gitlab, Knative, Deis, Dokku, and Drie.


### Cloud Native Buildpacks

* today: CNCF Sandbox project 

> Specification for turning applications into Docker images: [buildpacks.io](https://buildpacks.io/)

* Startup Time reduction because no fat jar
* Build packs integrated in Spring Boot from 2.3 on.


### Paketo Buildpacks?

* implementation for major languages (Java, Go, .Net, node.js, Ruby, PHP...)
* [paketo.io](https://paketo.io/)


### Maven/Gradle Plugin to use Paketo Buildpacks

The build-image plugin takes care of doing the Paketo build. From Spring Boot 2.3.x on simply run it with:

```shell script
mvn spring-boot:build-image
```



### Step by step...

Always start at [start.spring.io](start.spring.io) :)

![start-spring-io](screenshots/start-spring-io.png)

Implement your App (e.g. building a reactive Web app using Spring Webflux).

Then run the build with:

```shell script
mvn spring-boot:build-image
```

This will do a "normal" Maven build of your Spring Boot app, but also be 

```shell script
$ mvn spring-boot:build-image
...
[INFO] --- spring-boot-maven-plugin:2.4.0-M4:build-image (default-cli) @ spring-boot-buildpack ---
[INFO] Building image 'docker.io/library/spring-boot-buildpack:0.0.1-SNAPSHOT'
[INFO]
[INFO]  > Pulling builder image 'docker.io/paketobuildpacks/builder:base' 100%
[INFO]  > Pulled builder image 'paketobuildpacks/builder@sha256:00a9c25f8f994c1a044fa772f7e9314fe5d90d329b40f51426e1dafadbfa5ac8'
[INFO]  > Pulling run image 'docker.io/paketobuildpacks/run:base-cnb' 100%
[INFO]  > Pulled run image 'paketobuildpacks/run@sha256:21c1fb65033ae5a765a1fb44bfefdea37024ceac86ac6098202b891d27b8671f'
[INFO]  > Executing lifecycle version v0.9.2
[INFO]  > Using build cache volume 'pack-cache-604f3372716a.build'
[INFO]
[INFO]  > Running creator
[INFO]     [creator]     ===> DETECTING
[INFO]     [creator]     5 of 17 buildpacks participating
[INFO]     [creator]     paketo-buildpacks/bellsoft-liberica 4.0.0
[INFO]     [creator]     paketo-buildpacks/executable-jar    3.1.1
[INFO]     [creator]     paketo-buildpacks/apache-tomcat     2.3.0
[INFO]     [creator]     paketo-buildpacks/dist-zip          2.2.0
[INFO]     [creator]     paketo-buildpacks/spring-boot       3.2.1
[INFO]     [creator]     ===> ANALYZING
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/bellsoft-liberica:jre" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/bellsoft-liberica:jvmkill" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/bellsoft-liberica:helper" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/bellsoft-liberica:java-security-properties" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/executable-jar:class-path" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/spring-boot:spring-cloud-bindings" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/spring-boot:web-application-type" from app image
[INFO]     [creator]     Restoring metadata for "paketo-buildpacks/spring-boot:helper" from app image
[INFO]     [creator]     ===> RESTORING
[INFO]     [creator]     ===> BUILDING
[INFO]     [creator]
[INFO]     [creator]     Paketo BellSoft Liberica Buildpack 4.0.0
[INFO]     [creator]       https://github.com/paketo-buildpacks/bellsoft-liberica
[INFO]     [creator]       Build Configuration:
[INFO]     [creator]         $BP_JVM_VERSION              11.*            the Java version
[INFO]     [creator]       Launch Configuration:
[INFO]     [creator]         $BPL_JVM_HEAD_ROOM           0               the headroom in memory calculation
[INFO]     [creator]         $BPL_JVM_LOADED_CLASS_COUNT  35% of classes  the number of loaded classes in memory calculation
[INFO]     [creator]         $BPL_JVM_THREAD_COUNT        250             the number of threads in memory calculation
[INFO]     [creator]         $JAVA_TOOL_OPTIONS                           the JVM launch flags
[INFO]     [creator]       BellSoft Liberica JRE 11.0.8: Reusing cached layer
[INFO]     [creator]       Launch Helper: Reusing cached layer
[INFO]     [creator]       JVMKill Agent 1.16.0: Reusing cached layer
[INFO]     [creator]       Java Security Properties: Reusing cached layer
[INFO]     [creator]
[INFO]     [creator]     Paketo Executable JAR Buildpack 3.1.1
[INFO]     [creator]       https://github.com/paketo-buildpacks/executable-jar
[INFO]     [creator]       Process types:
[INFO]     [creator]         executable-jar: java org.springframework.boot.loader.JarLauncher
[INFO]     [creator]         task:           java org.springframework.boot.loader.JarLauncher
[INFO]     [creator]         web:            java org.springframework.boot.loader.JarLauncher
[INFO]     [creator]
[INFO]     [creator]     Paketo Spring Boot Buildpack 3.2.1
[INFO]     [creator]       https://github.com/paketo-buildpacks/spring-boot
[INFO]     [creator]       Creating slices from layers index
[INFO]     [creator]         dependencies
[INFO]     [creator]         spring-boot-loader
[INFO]     [creator]         snapshot-dependencies
[INFO]     [creator]         application
[INFO]     [creator]       Launch Helper: Reusing cached layer
[INFO]     [creator]       Web Application Type: Reusing cached layer
[INFO]     [creator]       Spring Cloud Bindings 1.6.0: Reusing cached layer
[INFO]     [creator]       4 application slices
[INFO]     [creator]       Image labels:
[INFO]     [creator]         org.opencontainers.image.title
[INFO]     [creator]         org.opencontainers.image.version
[INFO]     [creator]         org.springframework.boot.spring-configuration-metadata.json
[INFO]     [creator]         org.springframework.boot.version
[INFO]     [creator]     ===> EXPORTING
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/bellsoft-liberica:helper'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/bellsoft-liberica:java-security-properties'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/bellsoft-liberica:jre'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/bellsoft-liberica:jvmkill'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/executable-jar:class-path'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/spring-boot:helper'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/spring-boot:spring-cloud-bindings'
[INFO]     [creator]     Reusing layer 'paketo-buildpacks/spring-boot:web-application-type'
[INFO]     [creator]     Reusing 5/5 app layer(s)
[INFO]     [creator]     Reusing layer 'launcher'
[INFO]     [creator]     Reusing layer 'config'
[INFO]     [creator]     Adding label 'io.buildpacks.lifecycle.metadata'
[INFO]     [creator]     Adding label 'io.buildpacks.build.metadata'
[INFO]     [creator]     Adding label 'io.buildpacks.project.metadata'
[INFO]     [creator]     Adding label 'org.opencontainers.image.title'
[INFO]     [creator]     Adding label 'org.opencontainers.image.version'
[INFO]     [creator]     Adding label 'org.springframework.boot.spring-configuration-metadata.json'
[INFO]     [creator]     Adding label 'org.springframework.boot.version'
[INFO]     [creator]     *** Images (408f3d59f38e):
[INFO]     [creator]           docker.io/library/spring-boot-buildpack:0.0.1-SNAPSHOT
[INFO]
[INFO] Successfully built image 'docker.io/library/spring-boot-buildpack:0.0.1-SNAPSHOT'
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  20.009 s
[INFO] Finished at: 2020-10-27T14:29:46+01:00
[INFO] ------------------------------------------------------------------------
``` 

### Doing a Buildpack build on Travis

Simply add a [.travis.yml](.travis.yml) with

```yaml
language: java

jdk:
  - openjdk8
  - openjdk9
  - openjdk11

services:
  - docker

script: mvn clean spring-boot:build-image
```




### Links

https://spring.io/blog/2020/08/14/creating-efficient-docker-images-with-spring-boot-2-3
https://www.baeldung.com/spring-boot-docker-images