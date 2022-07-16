# Bookstack

I hosted my `wiki.mzfr.me` for several weeks on bookstack. I personally didn't like bookstack because most of my notes are static so I actually didn't needed the whole php+postgres setup. But that wasn't the only reason, another reason was I didn't find bookstack structure interesting. Managing things via shelves/books/chapters/pages were a bit weird to me. But again this is just my personal opinion.

P.S - I've moved my public notes from bookstack to [mkdocs](https://www.mkdocs.org/) with [Material theme](https://squidfunk.github.io/mkdocs-material/)

## How To

* If you have Portainer running then just build a new stack and copy paste the docker file attached below.
  - To see how to run portainer, read this(https://wiki.mzfr.me/self_hosting/portainer/)

* If you don't want to use portainer, save the docker content in a file called `docker-compose.yml`
  - Run `docker-compose up -d --build`
  - Make sure the docker containers started with: `docker ps -a`
  - Use `sudo` prefix to the commands if needed


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
      - DB_PASS=YOUR_PASSWORD_HERE #Change password
      - DB_DATABASE=bookstackapp
    volumes:
      - /data/bookstack:/config #Change /data/bookstack directory according to your own file structure
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
      - MYSQL_ROOT_PASSWORD=YOUR_PASSWORD_HERE #Change password
      - TZ=Asia/Kolkata 
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=YOUR_PASSWORD_HERE #Change password
    volumes:
      - /data/bookstack/DB:/config #Change /data/bookstack directory according to your own file structure
    restart: unless-stopped
```
