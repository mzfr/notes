# Syncthing

[Syncthing](https://syncthing.net/) is a file synchronization tool. Set it up on the server and tell it which file/folder to sync, give access to multiple devices, and takes care of the rest of the things.


## How to

* If you have Portainer running then just build a new stack and copy-paste the docker file attached below.
  - To see how to run portainer, read this(https://wiki.mzfr.me/self_hosting/portainer/)

* If you don't want to use portainer, save the docker content in a file called `docker-compose.yml`
  - Run `docker-compose up -d --build`
  - Make sure the docker containers started with: `docker ps -a`
  - Use `sudo` prefix to the commands if needed


```
version: "3.5"
services:
  syncthing:
    image: syncthing/syncthing
    container_name: syncthing
    hostname: syncthing
    environment:
      - PUID=1000 #Add your PUID
      - PGID=1000 #Add your PGID
      - TZ=Asia/Kolkata
    volumes:
      - <YOUR_PATH_HERE>/syncthing/config:/config #change the directories accordingly
      - <YOUR_PATH_HERE>/syncthing/sync:/data1 #change the directories accordingly
    ports:
      - 8384:8384
      - 22000:22000
      - 21027:21027/udp
    restart: unless-stopped
```

* Once the docker container is running, you'll find the application running on port 8384

## Personal view

This is an amazing application. I faced no issue in running this and it works amazingly. I use this to sync my notes across my server and phone. 