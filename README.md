# Maven multi module project example

## When specifying profile `build-cnb`

build app container image with spring-boot:boot-image

```bash
$ mvn -Pbuild-cnb clean package

$ docker images | grep -E '(foo|bar)-service'
com.example/foo-service       0.0.1-SNAPSHOT   e7efac599db6   41 years ago     270MB
com.example/bar-service       0.0.1-SNAPSHOT   6828f77cbc02   41 years ago     270MB
```

## When specifying profile `build-jib`

build app container image with jib:dockerBuild

```bash
$ $ mvn -Pbuild-jib clean package jib:dockerBuild

$ docker images | grep -E '(foo|bar)-service'
com.example/bar-service       0.0.1-SNAPSHOT   917b3d3d545f   51 years ago         151MB
com.example/foo-service       0.0.1-SNAPSHOT   04182bfb890d   51 years ago         151MB
```
