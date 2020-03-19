# Creating a Podman instance of JellyFin

```bash
podman run -d \
 --volume /opt/jellyfin/config:/config \
 --volume /opt/jellyfin/cache:/cache \
 --volume /media/plex:/media \
 - 8096:8096 \
 jellyfin/jellyfin
 ```
