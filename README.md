

### Language Support - Internationalization

To launch the desktop session in a different language, set the `LC_ALL` environment variable. For example:

*   `-e LC_ALL=zh_CN.UTF-8` - Chinese
*   `-e LC_ALL=ja_JP.UTF-8` - Japanese
*   `-e LC_ALL=ko_KR.UTF-8` - Korean
*   `-e LC_ALL=ar_AE.UTF-8` - Arabic
*   `-e LC_ALL=ru_RU.UTF-8` - Russian
*   `-e LC_ALL=es_MX.UTF-8` - Spanish (Latin America)
*   `-e LC_ALL=de_DE.UTF-8` - German
*   `-e LC_ALL=fr_FR.UTF-8` - French
*   `-e LC_ALL=nl_NL.UTF-8` - Netherlands
*   `-e LC_ALL=it_IT.UTF-8` - Italian

### docker-compose

```yaml
---
services:
  webtop:
    image: lscr.io/linuxserver/webtop:latest
    container_name: webtop
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config
    ports:
      - 3000:3000
      - 3001:3001
    shm_size: "1gb"
    restart: unless-stopped
```

### docker cli

```bash
docker run -d \
  --name=webtop \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 3000:3000 \
  -p 3001:3001 \
  -v /path/to/data:/config \
  --shm-size="1gb" \
  --restart unless-stopped \
  lscr.io/linuxserver/webtop:latest
```

## Parameters

Containers are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 3000:3000` | Web Desktop GUI HTTP, must be proxied |
| `-p 3001:3001` | Web Desktop GUI HTTPS |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-e TZ=Etc/UTC` | specify a timezone to use, see this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List). |
| `-v /config` | abc users home directory |
| `--shm-size=` | Recommended for all desktop images. |
