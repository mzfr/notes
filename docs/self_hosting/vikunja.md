# Vikunja

I was looking for a good To-Do list application and came across [vikunja](). I tried it and have found it to be really good.

## How to

* Make a separate folder named `vikunja`

* `docker-compose.yml`

```yml
version: '3'

services:
  db:
    image: mariadb:10
    command: --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
    environment:
      MYSQL_ROOT_PASSWORD: ROOT_RANDOM
      MYSQL_USER: vikunja
      MYSQL_PASSWORD: SQL_RANDOM_PASSWORD
      MYSQL_DATABASE: vikunja
    volumes:
      - /path/to/vikunja/db:/var/lib/mysql # path to your vikunja folder
    restart: unless-stopped
  api:
    image: vikunja/api
    environment:
      VIKUNJA_DATABASE_HOST: db
      VIKUNJA_DATABASE_PASSWORD: SQL_RANDOM_PASSWORD
      VIKUNJA_DATABASE_TYPE: mysql
      VIKUNJA_DATABASE_USER: vikunja
      VIKUNJA_DATABASE_DATABASE: vikunja
    ports:
      - 3456:3456
    volumes:
      - /path/to/vikunja/files:/app/vikunja/files # path to your vikunja folder
    depends_on:
      - db
    restart: unless-stopped
  frontend:
    image: vikunja/frontend
    ports:
      - 8973:80
    environment:
      VIKUNJA_API_URL: http://<YOU_IP>:3456/api/v1 # Add your IP/Domain
    restart: unless-stopped
```
* Go to portainer, click on stacks -> new stack and paste the above yaml file.
    - Read this([https://wiki.mzfr.me/books/applications/page/portainer](https://wiki.mzfr.me/books/applications/page/portainer)) to see how to setup portainer
* Click on deploy

If everything worked then you should be able to see your vikunja application on `<you_ip_or_domain>:8973`

### Using it with mobile application

Vikunja have a mobile application but its not very stable, I believe. So to be able to have a proper sync between mobile and the web application I use combination of [OpenTask]() and [Davx^5]().

You can download both of them from Google Play store or F-droid.