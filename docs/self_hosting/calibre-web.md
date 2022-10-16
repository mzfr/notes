```
version: "3.1"
services:
  calibre-web:
    image: lscr.io/linuxserver/calibre-web:latest
    container_name: calibre-web
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/kolkata
    volumes:
      - /home/mzfr/calibre/data:/config
      - /home/mzfr/calibre/library:/books
    ports:
      - 8083:8083
    restart: unless-stopped
```

Had to download the `metadata.db`(https://github.com/linuxserver/docker-calibre-web/issues/30#issuecomment-619478067) to get over the error. 

Then had to enable the uplaods - https://github.com/janeczku/calibre-web/issues/463#issuecomment-723523859