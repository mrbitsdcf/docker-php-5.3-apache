# PHP 5.3 Apache

PHP 5.3 [reached EOL](http://php.net/eol.php) on 14 Aug 2014 and thus, official docker support was [dropped](https://github.com/docker-library/php/pull/20). I still needed to run 5.3 so I built this image based on the latest official builds of PHP.

# What is PHP?

PHP is a server-side scripting language designed for web development, but which can also be used as a general-purpose programming language. PHP can be added to straight HTML or it can be used with a variety of templating engines and web frameworks. PHP code is usually processed by an interpreter, which is either implemented as a native module on the web-server or as a common gateway interface (CGI).

> [wikipedia.org/wiki/PHP](http://en.wikipedia.org/wiki/PHP)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/php/logo.png)

# How to use this image.

This is an image forked by [Eugene Ware](https://github.com/eugeneware/docker-php-5.3-apache) without WORKDIR and compilling PHP with ZLIB.

## With Command Line

For PHP projects run through the command line interface (CLI), you can do the following.

### Create a `Dockerfile` in your PHP project

    FROM mrbits/docker-php-5.3-apache
    COPY . /usr/src/myapp
    WORKDIR /usr/src/myapp
    CMD [ "php", "./your-script.php" ]

Then, run the commands to build and run the Docker image:

    docker build -t my-php-app .
    docker run -it --rm --name my-running-app my-php-app

### Run a single PHP script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a PHP script by using the PHP Docker image directly:

    docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp mrbits/docker-php-5.3-apache php your-script.php

### Installing modules

To install additional modules use a `Dockerfile` like this:

``` Dockerfile
FROM mrbits/docker-php-5.3-apache

# Installs curl
RUN docker-php-ext-install curl
```

Then build the image:

``` bash
$ docker build -t my-php .
```

### Without a `Dockerfile`

If you don't want to include a `Dockerfile` in your project, it is sufficient to do the following:

    docker run -it --rm --name my-php-fpm-app -v "$PWD":/var/www/html mrbits/docker-php-5.3-apache

## Credits

A big credit to [eugeneware](https://github.com/eugeneware/docker-php-5.3-apache) for first create this image. Eugene, you're the best!

A big credit to [helderco](https://github.com/helderco/docker-php-5.3) for the `fpm` version of this image.

# License

View [license information](http://php.net/license/) for the software contained in this image.
