Yii PHP Framework 2.0 container image
=====================================

This container image includes Yii PHP Framework version 2.0 with PHP version 7.2, and Apache HTTPd server version 2.4 based on Debian.

The container image is available on [Docker Hub](https://hub.docker.com/r/tomashavlas/yii2) as
`tomashavlas/yii2:2.0-debian9`.


Description
-----------

[Yii PHP Framework](http://www.yiiframework.com/) is a high-performance PHP framework best for developing Web 2.0 applications.

This container image provides containerized packaging of Yii PHP Framework 2.0 with PHP 7.2, and Apache HTTPd 2.4.
This image can be used as a base image for other applications based on Yii PHP Framework 2.0, 
image can be extended using [source-to-image](https://github.com/openshift/source-to-image) tool.


Usage
-----

This image can be used as a base image for other applications based on PHP.

This will create container named `yii2` running PHP with Apache HTTPd, serving data from `/wwwdata` directory.
Port `8080` will be exposed and mapped to the host.

```
$ docker run -d --name yii2 -p 8080:8080 -v /wwwdata:/srv/www:Z tomashavlas/yii2:2.0-debian9
```

This will create new Docker layered image named `yii2-app`, using source-to-image, while using data available in `/wwwdata` on the host.

```
$ s2i build file:///wwwdata tomashavlas/yii2:2.0-debian9 yii2-app
```

To run new image, simply execute:

```
$ docker run -d --name yii2 -p 8080:8080 yii2-app
```


S2I source repository layout
----------------------------

This image can be extended using source-to-image tool (see Usage section).

Application source code should be located in the root of the source directory.

**NOTE:**
This image extends S2I source repository layout of [PHP 7.2](https://github.com/tomashavlas/container-php-httpd/tree/master/7.2#s2i-source-repository-layout) container image.



Environment variables
---------------------

This images recognizes the following environment variables that can be set during initialization by passing `-e VAR=VALUE` to the Docker run command.

**NOTE:** 
This image includes support for environment variables defined by [PHP 7.2](https://github.com/tomashavlas/container-php-httpd/tree/master/7.2#environment-variables) container image.


Volumes
-------

The following mount points can be set by passing `-v /host/path:/container/path` to the Docker run command.

**`/srv/www`**

Yii PHP Framework application source directory.

**NOTE:** 
This image includes support for volumes defined by [PHP 7.2](https://github.com/tomashavlas/container-php-httpd/tree/master/7.2#volumes) container image.


Troubleshooting
---------------

The Yii PHP Framework in the container logs to the standard output by default, so the logs are available in container log.
The log can be examined by running:

```
$ docker logs <container>
```


See also
--------

Dockerfile and other sources for this container image are available on https://github.com/tomashavlas/container-yii2.
