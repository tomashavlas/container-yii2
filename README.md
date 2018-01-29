Yii PHP Framework container image
=================================

[![Build Stauts](https://api.travis-ci.org/tomashavlas/container-yii2.svg?branch=master)](https://travis-ci.org/tomashavlas/container-yii2/)

This repository contains Dockerfiles and scripts for Yii PHP Framework container images built on [PHP w/ Apache HTTPd](https://github.com/tomashavlas/container-php-httpd) container images based on Debian.


Versions
--------

Yii PHP Framework versions provided:

* [Yii 2.0](2.0)

PHP versions supported:

* PHP 7.2

Apache HTTPd versions supported:

* Apache HTTPd 2.4

Debian versions supported:

* Debian 9 "Stretch"


Installation
------------

* **Debain 9 based image**

    This image is available on DockerHub. To download it run:
    
    ```
    $ docker pull tomashavlas/yii2:2.0-debian9
    ```
    
    To build latest Debian based Yii PHP Framework image from source run:
    
    ```
    $ git clone --recursive https://github.com/tomashavlas/container-yii2
    $ cd container-yii2
    $ git submodule update --init
    $ make build TARGET=debian9 VERSION=2.0
    ```
    
To build other version of Yii PHP Framework just replace `2.0` value by particular version in commands above.

    
Usage
-----

For information about usage of Dockerfile for Yii PHP Framework 2.0 see [usage documentation](2.0).


Test
----

This repository also provides a test framework, which checks basic functionality of Yii PHP Framework image.

* **Debain 9 based image**

    ```
    $ cd container-yii2
    $ make test TARGET=debian9 VERSION=2.0
    ```


Credits
-------

This project is derived from official [Yii PHP Framework](https://github.com/yiisoft/yii2-docker) Docker image.
