# Prve nasadenie

```yaml
version: '3.1'

services:

  adminer:
    image: adminer
    restart: unless-stopped
    ports:
      - 8080:8080

  db:
    image: mysql:8
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: SuperTajneHeslo
```

```sh
docker-compose up
```

```sh
petos@prvy:~/work/network$ sudo ufw status
[sudo] password for petos:
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
```

```sh
petos@prvy:~/work/network$ sudo ufw allow proto tcp from any to any port 8080
Rule added
Rule added (v6)
petos@prvy:~/work/network$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
8080/tcp                   ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
8080/tcp (v6)              ALLOW       Anywhere (v6)
```

```yaml
  db:
    image: mysql:8
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: SuperTajneHeslo
    volumes:
      - ./mysql/data:/var/lib/mysql:rw
```

