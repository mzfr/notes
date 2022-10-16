# Calibre web

[Calibre web](https://hub.docker.com/r/linuxserver/calibre-web) is a web application with a good interface that allows you to browse/read books using the existing calibre database.

## How to

* If you have Portainer running then just build a new stack and copy-paste the docker file attached below.
  - To see how to run portainer, read this(https://wiki.mzfr.me/self_hosting/portainer/)

* If you don't want to use portainer, save the docker content in a file called `docker-compose.yml`
  - Run `docker-compose up -d --build`
  - Make sure the docker containers started with: `docker ps -a`
  - Use `sudo` prefix to the commands if needed


```docker
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
      - /home/mzfr/calibre/data:/config #change paths accordingly
      - /home/mzfr/calibre/library:/books #change paths accordingly
    ports:
      - 8083:8083
    restart: unless-stopped
```

### Some Common issues

* It's possible that when you try to access the application on port 8083 it gives the error **DB location is not valid, please enter correct path**
    - **SOLUTION** -> https://github.com/linuxserver/docker-calibre-web/issues/30#issuecomment-619478067

* By default the web reader and the upload option aren't enabled
    - **How to upload books** - https://github.com/janeczku/calibre-web/issues/463#issuecomment-723523859
    - **How to enable web reader** - https://github.com/janeczku/calibre-web/issues/1231#issuecomment-592141528

* It's also possible that uploading might not work, and in logs, it gives permission denied for the directories you mentioned in the docker-compose file. 
    - In this case, make sure that the paths given have the right permissions i.e both the `<YOUR_PATH>/calibre/data` and `<YOUR_PATH>/calibre/library` directories have the permissions of the user with ID 1000
    - Ex: I'm running docker-compose with PUID and PGID 1000, which is for a user named `mzfr`. Now both my directories `/home/mzfr/calibre/data` and `/home/mzfr/calibre/library` should have `mzfr:mzfr` in the permissions.

### Personal Opinion

I tried to host this just for fun and I didn't like it or it's not something that I want to keep hosted for myself. Things that I didn't like:

- Web reader isn't that good.
- If you want to do the conversion, etc you need to have calibre installed
    - I understand that this is obvious, but I expected it to have at least a basic small tool just for conversion.

>>>>>>> d0421d586499a33cac455399eb44d088a8d11596
