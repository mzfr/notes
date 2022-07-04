# Portainer

[Portainer](https://www.portainer.io/) is a container management system for Docker, Kubernetes, etc.

Using portainer can really make your life easier specially when you plan to host multiple applications in your homelab or on your VPS.

## How to 

I have [raspi 4](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) and I have installed [Arch Linux](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4) on it. Now since raspi have the ARM cores so the command varies for that one.

```bash
 sudo docker run -d -p 9000:9000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:linux-arm64
```

If you are hosting it on a VPS which is **NOT** ARM then you can just use the `latest` version of portainer.

```bash
 sudo docker run -d -p 9000:9000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```

With the above commands you are running the portainer container and supporting `http` protocol on port `9000` and `https` protocol on port 9443.