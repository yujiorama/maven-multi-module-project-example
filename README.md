# Maven multi module project example

## When specifying profile `build-cnb`

build app container image with spring-boot:boot-image

```bash
$ mvn -Pbuild-cnb clean package

$ docker images | grep -E '(foo|bar)-service'
com.example/foo-service       0.0.1-SNAPSHOT   e7efac599db6   41 years ago     270MB
com.example/bar-service       0.0.1-SNAPSHOT   6828f77cbc02   41 years ago     270MB

$ docker run --rm -it --entrypoint /layers/paketo-buildpacks_bellsoft-liberica/jre/bin/java com.example/bar-service:0.0.1-SNAPSHOT --version
openjdk 11.0.10 2021-01-19 LTS
OpenJDK Runtime Environment (build 11.0.10+9-LTS)
OpenJDK 64-Bit Server VM (build 11.0.10+9-LTS, mixed mode)
```

## When specifying profile `build-jib`

build app container image with jib:dockerBuild

```bash
$ $ mvn -Pbuild-jib clean package

$ docker images | grep -E '(foo|bar)-service'
com.example/bar-service       0.0.1-SNAPSHOT   917b3d3d545f   51 years ago         151MB
com.example/foo-service       0.0.1-SNAPSHOT   04182bfb890d   51 years ago         151MB

$ docker run --rm -it com.example/bar-service:0.0.1-SNAPSHOT --version
openjdk 11.0.10 2021-01-19 LTS
OpenJDK Runtime Environment (build 11.0.10+9-LTS)
OpenJDK 64-Bit Server VM (build 11.0.10+9-LTS, mixed mode)
```

## (Example) plain distroless/java:11

* size
    - Bigger than image with cnb-build
    - Bigger than iamge with jib-build
* version
    - Older than image with cnb-build
    - Older than iamge with jib-build

```bash
$ docker pull gcr.io/distroless/java:11
$ docker images | grep gcr.io/distroless/java
gcr.io/distroless/java            11               358e33e4868e   51 years ago     197MB

$ docker run --rm -it gcr.io/distroless/java:11 --version
openjdk 11.0.6 2020-01-14
OpenJDK Runtime Environment (build 11.0.6+10-post-Debian-1bpo91)
OpenJDK 64-Bit Server VM (build 11.0.6+10-post-Debian-1bpo91, mixed mode)
```
