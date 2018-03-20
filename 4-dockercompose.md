docker-compose.yml

```
version: "2"
services:
    wordpress:
        image: wordpress:4.7.0
        container_name: wordpress
        ports:
            - "9000:80"
        depends_on:
            - db
        environment:
            WORDPRESS_DB_HOST: "db:3306"
        env_file: .env
    db:
        image: mysql:latest
        container_name: mysql
        env_file: .env
        ports:
            - "3306:3306"

```

.env

```
WORDPRESS_DB_NAME=wordpress
WORDPRESS_DB_USER=wp_user
WORDPRESS_DB_PASSWORD=hogehoge

MYSQL_RANDOM_ROOT_PASSWORD=yes
MYSQL_DATABASE=wordpress
MYSQL_USER=wp_user
MYSQL_PASSWORD=hogehoge
```
