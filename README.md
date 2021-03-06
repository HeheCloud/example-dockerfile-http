# Dockerfile方式部署应用快速入门指南

本指南将引导您在HeheCloud中通过`dockerfile`方式部署一个应用

## 使用

### 创建应用

```console
$ git clone https://github.com/HeheCloud/example-dockerfile-http.git
$ cd example-dockerfile-http
$ deis create dockerfile-hello
Creating application... done, created dockerfile-hello
Git remote deis added
```

### 通过`git push`部署应用

```
$ git push deis master
Counting objects: 17, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (17/17), 1.45 KiB | 0 bytes/s, done.
Total 17 (delta 0), reused 0 (delta 0)

-----> Building Docker image
remote: build context to Docker daemon 14.34 kB
remote: build context to Docker daemon
Step 0 : FROM alpine:3.1
 ---> 878b6301beda
Step 1 : RUN apk add -U         bash    nginx   && rm -rf /var/cache/apk*
 ---> Running in b102ad65858e
fetch http://dl-4.alpinelinux.org/alpine/v3.1/main/x86_64/APKINDEX.tar.gz
(1/6) Installing ncurses-terminfo-base (5.9-r3)
(2/6) Installing ncurses-libs (5.9-r3)
(3/6) Installing readline (6.3-r3)
(4/6) Installing bash (4.3.30-r0)
(5/6) Installing pcre (8.36-r2)
(6/6) Installing nginx (1.6.2-r1)
Executing nginx-1.6.2-r1.pre-install
Executing busybox-1.22.1-r15.trigger
OK: 8 MiB in 21 packages
 ---> a42c69c8166d
Removing intermediate container b102ad65858e
Step 2 : RUN ln -sf /dev/stdout /var/log/nginx/access.log
 ---> Running in 222ef65b2bc8
 ---> 8e842b2ddac9
Removing intermediate container 222ef65b2bc8
Step 3 : RUN ln -sf /dev/stderr /var/log/nginx/error.log
 ---> Running in 827ea0fbdaca
 ---> 0072af10d448
Removing intermediate container 827ea0fbdaca
Step 4 : ENV POWERED_BY Hehecloud
 ---> Running in 5e02d3a7623a
 ---> d5dc43a1857c
Removing intermediate container 5e02d3a7623a
Step 5 : COPY rootfs /
 ---> dfd0ec3bf508
Removing intermediate container cd988893ffa9
Step 6 : CMD /bin/boot
 ---> Running in 84bf0178054d
 ---> c486f41ee92f
Removing intermediate container 84bf0178054d
Step 7 : EXPOSE 80
 ---> Running in dc0e3ef32941
 ---> ac23f7a495fc
Removing intermediate container dc0e3ef32941
Step 8 : ENV GIT_SHA 902c232bc9a382013e5b6a14b586e907cb8bc3bc
 ---> Running in 6a9ea2dadf80
 ---> e65fef6110cf
Removing intermediate container 6a9ea2dadf80
Successfully built e65fef6110cf
-----> Pushing image to private registry

-----> Launching...
       done, dockerfile-hello:v2 deployed to Deis

       http://dockerfile-hello.6a9ea.heheapp.com

       To learn more, use `deis help` or visit http://deis.io

To ssh://git@deis.6a9ea.deisapp.com:2222/dockerfile-hello.git
 * [new branch]      master -> master
$ curl http://dockerfile-hello.6a9ea.heheapp.com
Powered by HeheCloud
```

### 设置环境变量

```
$ deis config:set POWERED_BY="HaHaHa"
Creating config... done, v4

=== php-hello
DEIS_APP: dockerfile-hello
POWERED_BY: HaHaHa
```

### 测试环境变量是否生效

```
$ curl http://dockerfile-hello.6a9ea.heheapp.com
Powered by HaHaHa
```

## 更多资源

* [HeheCloud](http://hehecloud.com/)
* [Deis中文指南](http://deis.heheapp.com/)
