# Nginx Proxy Manager

I came across [nginx proxy manager](https://nginxproxymanager.com/) when I was trying to look into some simple and good proxy manager and was thinking of using [traefik](https://traefik.io/). Now I'm not aware of all the PROs and Cons of both of these tools but I've found the Nginx proxy manager more useful than traefik or any other tool.

The GUI in Nginx proxy manager makes everything really easy(EZ).

## How to

* Make a separate directory for this.
    - I created a directory named `nginx_proxy_manager`

* Now use the `docker-compose.yml` below

```docker-compose
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "sql_admin"
      DB_MYSQL_PASSWORD: "COMPLEX_PASSWORD_HERE"
      DB_MYSQL_NAME: "proxy_db"
    volumes:
      - /home/nginx_proxy_manager/NpM_data:/data # Change the path to directory you created in step 1.
      - /home/nginx_proxy_manager/letsencrypt:/etc/letsencrypt # Change the path to directory you created in step 1
  db:
    image: 'jc21/mariadb-aria:latest'
    environment:
      MYSQL_ROOT_PASSWORD: 'COMPLEX_PASSWORD_HERE'
      MYSQL_DATABASE: 'proxy_db'
      MYSQL_USER: 'sql_admin'
      MYSQL_PASSWORD: 'COMPLEX_PASSWORD_HERE'
    volumes:
      - /home/nginx_proxy_manager/mysql:/var/lib/mysql1 # Change the path to directory you created in step 1
```

Feel free to change the `MYSQL` Passwords.

Now if you are using portainer, then simply go to your portainer instance and click on `stacks` -> `New stack`. Enter the name of the stack like `nginx proxy manager`, copy-paste the above docker-compose there, and simply click on `update stack` or `deploy stack`.

If everything goes well, then you should have the proxy manager running on port `81`(`<YOUR_IP>:81`) and for the first time log in you can use:
    
   * Email - `admin@example.com`
   * Password - `changeme`