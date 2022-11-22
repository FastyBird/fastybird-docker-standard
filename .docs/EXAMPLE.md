```yaml
services:
    app:
        image: fastybird/standard:1.0-traditional-alpine
        environment:
            PHP_DATE_TIMEZONE: "Europe/Prague"
        volumes:
            - ./:/app:delegated
            - ./.docker/dev/php.ini:/etc/php8/php.ini:delegated
        ports:
            - 80:80
        networks:
            - fastybird
```