## training plan 

<img src="plan.png">

## FInal docker compose example with Dockerfile 

### Dockerfile for java webapp springboot 

### clone app 

```
git clone  https://github.com/redashu/java-springboot.git
```

### java based app build and run 

<img src="appb.png">

### Dockerfile multistage 

```
FROM oraclelinux:8.4 AS build-stage
LABEL name=ashutoshh
RUN yum install maven java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64 -y
RUN mkdir /javaapp
COPY . /javaapp/
WORKDIR /javaapp
RUN mvn clean package
# output of above command target/WebApp.war 
FROM tomcat 
LABEL email=ashutoshh@linux.com 
COPY --from=build-stage /javaapp/target/WebApp.war /usr/local/tomcat/webapps/ 
EXPOSE 8080 

```

### .dockerignore

```
Dockerfile
.dockerignore
*.md
LICENSE
.git
```

### java-compose.yaml file 

```
version: '3.8'
services:
  ashuapp6:
    image: ashutomcat:v1 # this image will be build  
    build:  # build docker image 
      context: java-springboot # location of dockerfile 
    container_name: ashuc11111
    ports:
    - "1009:8080"
```

### running compose 

```
docker-compose -f  java-compose.yaml  up -d --build 
[+] Building 5.2s (6/13)                                                                           
 => [stage-1 1/2] FROM docker.io/library/tomcat@sha256:acbf4ace21d5a9bfca00865e615b3061c262b  4.8s
 => => sha256:d78b22b857e23a35f3f650f71006a3a0adf5bdd7d04896e916758fb645f88a 2.42kB / 2.42kB  0.0s
 => => sha256:52b67ab29b7461505b67976af1447cb3da0651874fd5d5466a75ba246dcd 12.85kB / 12.85kB  0.0s
 => => sha256:6d5c91c4cd86dde23108ab3af91e9eae838d0059a380ee7dfd4f370b6d98 54.58MB / 54.58MB  0.8s
 => => sha256:5e20d165240e4863f511ba9a1b730a75630545413cc7fee0c9eca825a3ad6b 5.42MB / 5.42MB  0.3s
 => => sha256:1334d60df9a8ba9ff6e8bf5f468941149156415ec2f1550d096a40e0fbdf096a 210B / 210B    0.3s
 => => sha256:16c2728dcd90d369747683d3c2de195d565c3f3
```

### 

```
[ashu@docker-client ashu-compose]$ docker-compose -f  java-compose.yaml ps
NAME                COMMAND             SERVICE             STATUS              PORTS
ashuc11111          "catalina.sh run"   ashuapp6            running             0.0.0.0:1009->8080/tcp, :::1009->8080/tcp
```

## Dockerfile - build -test / run / remove  after changes in source code 

### Intro continious Integration  (CI)

<img src="ci.png">

## build image from gitrepo -- manually 

```
 docker build  -t  ashuciapp:testv1  https://github.com/redashu/mobi-ashuapp.git 
Sending build context to Docker daemon   5.12kB
Step 1/3 : FROM nginx
latest: Pulling from library/nginx
42c077c10790: Pull complete 
62c70f376f6a: Pull complete 
915cc9bd79c2: Pull complete 
75a963e94de0: Pull complete 
7b1fab684d70: Pull complete 
db24d06d5af4: Pull complete 
Digest: sha256:2bcabc23b45489fb0885d69a06ba1d648aeda973fae7bb981bafbb884165e514
Status: Downloaded newer image for nginx:latest
 ---> 0e901e68141f
Step 2/3 : LABEL name=ashutoshh
 ---> Running in 47a4ab5523a0
Removing intermediate container 47a4ab5523a0
 ---> f478901e4493
Step 3/3 : COPY . /usr/share/nginx/html/
 ---> 6eb89dc167cb
Successfully built 6eb89dc167cb
Successfully tagged ashuciapp:testv1
[ashu@docker-client mobi-dockerimages]$ 
```

### Jenkins for automated CI 

### Jenkins installation link 

[install](https://www.jenkins.io/doc/book/installing/)



## problem in containers  wrt Container runtimes 

<img src="prob.png">

### options for solutions 

<img src="sol1.png">

### Introduction to kubernetes -- 

<img src="k8s.png">

### k8s infra setup 

<img src="k8sinfo.png">







