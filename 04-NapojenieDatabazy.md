# Demo guestbook pouzivajuci databazu

```
petos@prvy:~/work/network/php-demo/src$ wget https://code-boxx.com/wp-content/uploads/2022/10/guest-book-php.zip
...

unzip guest-book-php.zip
```

V Admineri vytvoríme novú databázu `phpdemo` s nasledujúcou tabuľkou:
```sql
CREATE TABLE `guestbook` (
  `post_id` bigint(20) NOT NULL,
  `email` varchar(255) NOT NULL,
  `name` varchar(255) NOT NULL,
  `comment` text NOT NULL,
  `datetime` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

ALTER TABLE `guestbook`
  ADD PRIMARY KEY (`post_id`,`email`),
  ADD KEY `datetime` (`datetime`);
```

```sh
petos@prvy:~/work/network$ vim ./2-lib.php
```

```php
// (E) DATABASE SETTINGS - CHANGE TO YOUR OWN !
define("DB_HOST", "db");
define("DB_NAME", "phpdemo");
define("DB_CHARSET", "utf8");
define("DB_USER", "root");
define("DB_PASSWORD", "SuperTajneHeslo");
```

```sh
petos@prvy:~/work/network$ vim ./php-demo/Dockerfile
```

```docker
FROM php:8-apache

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql

COPY src/ /var/www/html/
```

```sh
docker-compose up --build
```

http://prvy.kontainer.tk:8081/3-page.php