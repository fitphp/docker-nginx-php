## 构建多平台

### 8-fpm-alpine
```
docker buildx build --push --platform linux/arm64,linux/amd64 -t bincent/php:8-fpm-alpine .
```

``` 7.4-fpm-alpine
docker buildx build --push --platform linux/arm64,linux/amd64 -t bincent/php:7.4-fpm-alpine .
```