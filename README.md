# Joomla project template

Joomla website is running in Docker environment.

### Stack
- PHP 8.4.3 (FPM)
- Joomla 6
- Nginx
- Maria DB 11.2
- Adminer (optional)

### Quick start

- Copy joomla app in `joomla` folder.
- Edit `docker/nginx.conf` file: replace example.org domain
- Copy `.env.example` to `.env`, edit
- `docker compose up -d`

### Optional Adminer

Adminer runs under the `tools` Compose profile, so it starts only when that
profile is active. `COMPOSE_PROFILES=tools` in `.env` turns it on; an empty or
missing value leaves it out, which is what you usually want in production.

Start it once without changing `.env`:

```shell
docker compose up -d adminer
```

Adminer and MariaDB listen on `127.0.0.1` only. On a remote server, reach
them through an SSH tunnel:

```shell
ssh -L 8090:127.0.0.1:8090 user@server   # then open http://localhost:8090
```

### How to renew Let's encrypt certificate

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