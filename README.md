# Joomla project template

Joomla website is running in Docker environment.

### Stack
- PHP 8.3.1
- Joomla 5
- Nginx
- Maria DB 11.2
- Adminer

### Quick start

- Copy joomla app in `joomla` folder.
- Edit `docker/nginx.conf` file: replace example.org domain
- Copy `.env.example` to `.env`, edit
- `docker compose up -d`



### Hot to renew Let's encrypt certificate

Docker-compose already has certbot container you can use, just execute:

```shell
docker compose run --rm certbot renew
```

### Add certificate renew in cron

```shell
crontab -e
```

Add this line, it will run certbot renew every second month:
```text
0 0 1 */2 * docker compose run --rm certbot renew
```