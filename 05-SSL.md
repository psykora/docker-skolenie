Add to docker-compose.yaml
```yaml
  nginx:
    image: nginx:latest
    ports:
      - 80:80
      - 443:443
    restart: always
    volumes:
      - ./nginx/conf.d/:/etc/nginx/conf.d/:ro
      - ./certbot/www:/var/www/certbot/:ro
      - ./certbot/conf/:/etc/nginx/ssl/:ro

  certbot:
    image: certbot/certbot:latest
    volumes:
      - ./certbot/www/:/var/www/certbot/:rw
      - ./certbot/conf/:/etc/letsencrypt/:rw
```

```
nginx/conf.d/prvy.kontainer.tk.conf
```

```
# prvy.kontainer.tk
upstream prvy.kontainer.tk {
        server php-demo:80;
}

log_format vhost '$host $remote_addr - $remote_user [$time_local] '
                 '"$request" $status $body_bytes_sent '
                 '"$http_referer" "$http_user_agent"';

server {
        server_name prvy.kontainer.tk;
        server_tokens off;
        listen 80;
        location /.well-known/acme-challenge/ {
                root /var/www/certbot;
        }
        access_log /var/log/nginx/access.log vhost;
        location / {
                return 301 https://$host$request_uri;
        }
}
server {
        server_name prvy.kontainer.tk;
        listen 443 ssl http2;
        access_log /var/log/nginx/access.log vhost;

        ssl_certificate /etc/nginx/ssl/live/prvy.kontainer.tk/fullchain.pem;
        ssl_certificate_key /etc/nginx/ssl/live/prvy.kontainer.tk/privkey.pem;

        location / {
                proxy_pass http://prvy.kontainer.tk;
        }
}
```

```
docker-compose up nginx
```

```
docker-compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ -d prvy.kontainer.tk
```

```
docker-compose up
```


