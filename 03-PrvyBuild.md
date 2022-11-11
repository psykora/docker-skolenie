# Prvý build

```sh
petos@prvy:~/work/network$ mkdir -p ./php-demo/src
petos@prvy:~/work/network$ vim ./php-demo/src/index.php
```

```php
<?php
phpinfo();
?>
```

```sh
petos@prvy:~/work/network$ vim ./php-demo/Dockerfile
```

```dockerfile
FROM php:8-apache
COPY src/ /var/www/html/
```

```yaml
# Add to docker-compose.yaml

  php-demo:
    build: ./php-demo
    restart: unless-stopped
    ports:
      - 8081:80
```

```
petos@prvy:~/work/network$ docker-compose up
Building php-demo
...
```

```sh
petos@prvy:~/work/network/mysql/data$ sudo ufw allow proto tcp from any to any port 8081
Rule added
Rule added (v6)
petos@prvy:~/work/network/mysql/data$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
8080/tcp                   ALLOW       Anywhere
8081/tcp                   ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
8080/tcp (v6)              ALLOW       Anywhere (v6)
8081/tcp (v6)              ALLOW       Anywhere (v6)
```

http://prvy.kontainer.tk:8081/