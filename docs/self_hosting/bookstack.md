**INCOMPLETE**


```docker
version: "3"
services:
  bookstack:
    image: linuxserver/bookstack
    container_name: bookstack
    environment:
      - PUID=1000
      - PGID=1000
      - DB_HOST=bookstack_db
      - DB_USER=bookstack
      - DB_PASS=YOUR_PASSWORD_HERE
      - DB_DATABASE=bookstackapp
    volumes:
      - /data/bookstack:/config
    ports:
      - 6875:80
    restart: unless-stopped
    depends_on:
      - bookstack_db
  bookstack_db:
    image: linuxserver/mariadb
    container_name: bookstack_db
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=YOUR_PASSWORD_HERE
      - TZ=Asia/Kolkata 
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=YOUR_PASSWORD_HERE
    volumes:
      - /data/bookstack/DB:/config
    restart: unless-stopped
```