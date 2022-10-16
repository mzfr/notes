# tt-rss

I was using feedly and it was doing the decent job but then I felt that since I have the resources I should try to self host the RSS reader. Even though there are [numerous feed readers](https://github.com/awesome-selfhosted/awesome-selfhosted#feed-readers) I felt that [tt-rss](https://tt-rss.org/) is the most simplest one out there.

## How to


```yml
version: "3"
services:
  service.rss:
    image: wangqiru/ttrss:latest
    container_name: ttrss
    ports:
      - 7869:80
    environment:
      - SELF_URL_PATH=http://your.domain.here/ # please change to your own domain
      - DB_PASS=SAME_PASSWORD_HERE_AS_WELL # use the same password defined in `database.postgres`
      - PUID=1000
      - PGID=1000
    volumes:
      - /home/ttrs/feed-icons:/var/www/feed-icons/
    networks:
      - public_access
      - service_only
      - database_only
    stdin_open: true
    tty: true
    restart: always

  service.mercury: # set Mercury Parser API endpoint to `service.mercury:3000` on TTRSS plugin setting page
    image: wangqiru/mercury-parser-api:latest
    container_name: mercury
    networks:
      - public_access
      - service_only
    restart: always

  service.opencc: # set OpenCC API endpoint to `service.opencc:3000` on TTRSS plugin setting page
    image: wangqiru/opencc-api-server:latest
    container_name: opencc
    environment:
      - NODE_ENV=production
    networks:
      - service_only
    restart: always

  database.postgres:
    image: postgres:13-alpine
    container_name: postgres
    environment:
      - POSTGRES_PASSWORD=SAME_PASSWORD_HERE_AS_WELL # feel free to change the password
    volumes:
      - /home/ttrs/postgres/data/:/var/lib/postgresql/data # persist postgres data to ~/postgres/data/ on the host
    networks:
      - database_only
    restart: always

volumes:
  feed-icons:

networks:
  public_access: # Provide the access for ttrss UI
  service_only: # Provide the communication network between services only
    internal: true
  database_only: # Provide the communication between ttrss and database only
    internal: true
```

* I had created a new directory named `ttrss` for storing all the tt-rss stuff. 
* In order to find your PUID and PGID you can run `id` command 

Now just go to your portainer instance and click on `stacks -> new stack`, enter the name of the stack(anything you like), paste the docker-compose and click on the deploy button.

* To see how to setup portainer, read this - [Installing portainer](https://wiki.mzfr.me/self_hosting/portainer/)

If everything was done correctly then you should have tt-rss running on `<youIP>:7869`. 

### Feedly Theme & import (optional)


#### Importing from Feedly.com

If you want you can import opml from feedly to your self hosted instance of tt-rss.

* Go to [https://feedly.com/i/organize](https://feedly.com/i/organize)
    - Login if needed
* Then click on the export button
    - The export button is right beside the `Import OPML` button, its a small arrow type symbol
* Download your feedly opml
* Go to your tt-rss instance
    - Go to preferences -> Feeds -> OPML
    - Then just import the OPML file you exported from feedly.

#### Theme

I prefer feedly theme in tt-rss. So if you want that just follow the steps below:

* Login into your tt-rss instance
    - For first time login use 
        - Username: `admin`
        - Password: `password`

* Go to prefrences
    - In top right there are 3 bars click on them to see preferences option

* In `General` there is a drop down to select the new theme