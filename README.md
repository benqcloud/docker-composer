## About `benqcloud/composer`

It is a PHP composer runtime

## Installing Composer Dependencies For Existing Applications

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    ghcr.io/benqcloud/composer:php71-v1 \
    composer install --ignore-platform-reqs
```

## Use as builder image in Dockerfile

```dockerfile
### builder stage
FROM ghcr.io/benqcloud/composer:php71-v1 AS composer-builder

WORKDIR /var/www/html

COPY . /var/www/html
RUN composer install --optimize-autoloader --no-dev --ignore-platform-reqs

### runtime stage
FROM ghcr.io/benqcloud/docker-laravel:php71

WORKDIR /var/www/html

COPY --from=composer-builder --chown=www-data:www-data /var/www/html /var/www/html
```
