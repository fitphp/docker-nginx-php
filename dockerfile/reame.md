## 构建多平台

### 准备构建多平台
```
$ docker buildx create --name mybuilder --driver docker-container

$ docker buildx use mybuilder
```

###
8.0 以下版本 不支持linux/arm64

### 构建多平台各版本
```
// V7
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:7-fpm-alpine .
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:7.3-fpm-alpine .
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:7.4-fpm-alpine .

// V8
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:8-fpm-alpine .
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:8.0-fpm-alpine .
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:8.1-fpm-alpine .
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:8.2-fpm-alpine .

// latest
$ docker buildx build --push --platform linux/386,linux/amd64,linux/arm/v7 -t bincent/php:fpm-alpine .
```