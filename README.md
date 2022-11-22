![FastyBird Docker Standard](.docs/assets/fastybird-docker-readme.png)

# FastyBird Docker Standard

## Introduction

The FastyBird Docker Standard is a docker base image available for everyone as part of [FastyBird](https://www.fastybird.com) [IoT](https://en.wikipedia.org/wiki/Internet_of_things) [Open Source](https://en.wikipedia.org/wiki/Open_source).
The key idea of these tools is to provide one image shared between environments.
Feel free to fork, extend or copy source files.

### Features:

#### 1. Choosable images

We decided to use two most popular/known Linux distributions - Ubuntu and Alpine.
On top of these distributions we created our easy extendable images.

#### 2. All in one

All images are created with PHP support with [PHP-FPM](https://www.php.net/manual/en/install.fpm.php) and with many extensions and production-ready configuration.
[NGINX](https://www.nginx.com) is here as a reverse proxy, and traditional images are also with [Node.js](https://nodejs.dev/en/) for building a frontend.

#### 3. Single Stage Build

We wanted to keep these images and their usage as simply as possible even for user which are starting their journey with Docker.
So we decided to go with single stage build. 

#### 4. [KISS Principle](https://en.wikipedia.org/wiki/KISS_principle)

## Metadata

| Image                     | Size                                                                                  |
|---------------------------|---------------------------------------------------------------------------------------|
| `1.0-traditional`        | ![Docker Hub](https://badgen.net/docker/size/fastybird/standard/1.0-traditional)        |
| `1.0-traditional-alpine` | ![Docker Hub](https://badgen.net/docker/size/fastybird/standard/1.0-traditional-alpine) |
| `1.0-headless`           | ![Docker Hub](https://badgen.net/docker/size/fastybird/standard/1.0-headless)           |

> Please note that image sizes may differ in each architecture.

## Supported Architectures
* linux/amd64
* linux/arm64
* linux/arm/v7
* linux/arm/v8

> Proudly hosted on [Docker Hub](https://hub.docker.com/r/fastybird/standard)

## Images

### Traditional

The Traditional image is everything you require to run a traditional IoT platform on [FastyBird](https://www.fastybird.com).
The image contains PHP, NGiNX, and Node.js compatible with the FastyBird version.
Example [FastyBird](https://www.fastybird.com) `1.0` will work best with `fastybird/standard:1.0-traditional` image.

### Headless

Headless image is getting more and more popular. The Headless image is a node-less Traditional image that will save you some space when you would like to use [FastyBird](https://www.fastybird.com) as a service.

## Feedback

Use [mail](mailto:code@fastybird.com) or [Tweet](https://twitter.com/fastybird) us for any idea that can improve the
project.