# jboss-eap-7.2 [![Build Status](https://travis-ci.org/daggerok/jboss-eap-7.2.svg?branch=master)](https://travis-ci.org/daggerok/jboss-eap-7.2)
Patched JBoss EAP 7.2 (including __7.2.5 patch__) Docker automation build based on centos8 / alpine3.9 images

[daggerok/jboss-eap-7.2](https://hub.docker.com/r/daggerok/jboss-eap-7.2/)

## available tags

- [latest](https://github.com/daggerok/jboss-eap-7.2/blob/master/Dockerfile)

- [7.2.5-alpine](https://github.com/daggerok/jboss-eap-7.2/blob/7.2.5-alpine/Dockerfile)
- [7.2.5-centos](https://github.com/daggerok/jboss-eap-7.2/blob/7.2.5-centos/Dockerfile)

- [7.2.0-alpine](https://github.com/daggerok/jboss-eap-7.2/blob/7.2.0-alpine/Dockerfile)
- [7.2.0-centos](https://github.com/daggerok/jboss-eap-7.2/blob/7.2.0-centos/Dockerfile)

## usage

```Dockerfile
FROM daggerok/jboss-eap-7.2:7.2.5-alpine
COPY --chown=jboss ./target/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war
```

## health check

```Dockerfile
FROM daggerok/jboss-eap-7.2:7.2.5-alpine
HEALTHCHECK --retries=33 \
            --timeout=1s \
            --interval=1s \
            --start-period=3s \
            CMD wget -q --spider http://127.0.0.1:8080/my-service/health || exit 1
# ...
```

## multi deployment

```Dockerfile
FROM daggerok/jboss-eap-7.2:7.2.5-centos
# ...
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/
```

## remote debug

```Dockerfile
FROM daggerok/jboss-eap-7.2:7.2.5-alpine
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
EXPOSE 5005
# ...
```

## exposing ports

- management: `9990`
- web http: `8080`
- https: `8443`

## web administration

- username: `admin`
- password: `Admin.123`

<!--

git reset --hard origin/master
git fetch -p -a --prune-tags --force --tags 

git tag -d $tagName
git push --delete origin $tagName

release workflow history:

git tag 7.2.0-centos
git push origin --tags --force

git tag 7.2.0-alpine
git push origin --tags --force

git tag 7.2.5-centos
git push origin --tags

git tag 7.2.5-alpine
git push origin --tags

-->
