# [benqcloud/composer](https://github.com/benqcloud/docker-composer)

![docker-publish](https://github.com/benqcloud/docker-composer/actions/workflows/docker-publish.yml/badge.svg)

It is a PHP composer runtime

## Supported Architectures

| Architecture | Available
| :----: | :----: |
| x86-64 | ✅ |
| arm64 | ✅ |

## Usage

### docker-cli

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -e HOME=/var/www/html \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    ghcr.io/benqcloud/composer:php-8.1 \
    composer install --ignore-platform-reqs
```

### Use as builder image in Dockerfile

```dockerfile
### builder stage
FROM ghcr.io/benqcloud/composer:php-8.1 AS composer-builder

WORKDIR /var/www/html

COPY . /var/www/html
RUN composer install --optimize-autoloader --no-dev --ignore-platform-reqs

### runtime stage
FROM ghcr.io/benqcloud/docker-laravel:php-8.1-apache

WORKDIR /var/www/html

COPY --from=composer-builder --chown=www-data:www-data /var/www/html /var/www/html
```
