# Welcome to QuasiTVSync

**QuasiTVSync** is the dedicated self-hosted backend server for [QuasiTV](https://www.quasitv.app). It acts as the central hub for your network, seamlessly synchronizing your viewing experience across all your Android and Google TV devices.  Currently in closed alpha, but will be available to the public soon.

Never lose your place or have to manually recreate your custom channel lineups again. Set it up once, and let QuasiTVSync handle the rest.

**Requires QuasiTV Ultimate In App Purchase**

---

## Core Features

* **Real-Time Synchronization:** Instantly sync profiles, channels, and schedule across every connected client.
* **Access Control:** Only authorized users and devices can access your self-hosted server. (Multiple users planned for future update)
* **Lightweight Architecture:** Powered by a highly efficient backend, QuasiTVSync runs quietly and efficiently on your self-hosted hardware without draining system resources.

---

## Installation & Setup

You can run QuasiTVSync using either standard Docker CLI commands or Docker Compose.

### Option 1: Docker CLI

Run the following command to start the container, replacing the `/path/to/your/...` directories with your actual host paths:

```bash
docker run -d \
       --name=quasitv-sync \
       -p 26988:26988 \
       -p 51234:51234 \
       -e PUID=1000 \
       -e PGID=1000 \
       -v /path/to/your/settings:/settings \
       -v /path/to/your/data:/data \
       --restart unless-stopped \
       ghcr.io/gonemadsoftware/quasitv-sync:latest
```

**Note:** quasitv-sync needs read and write access to the locations you are mounting to /settings and /data

```bash
chmod 755 /path/to/your/settings
chmod 755 /path/to/your/data
```

### Option 2: Docker Compose

If you prefer using Docker Compose, create a docker-compose.yml file with the following configuration:

```yaml
services:
  quasitv-sync:
    image: ghcr.io/gonemadsoftware/quasitv-sync:latest
    container_name: quasitv-sync
    ports:
      - "26988:26988"
      - "51234:51234"
    environment:
      - PUID=1000
      - PGID=1000
    volumes:
      - /path/to/your/settings:/settings
      - /path/to/your/data:/data
    restart: unless-stopped
```

```bash
docker compose up -d
```

**Note:** quasitv-sync needs read and write access to the locations you are mounting to /settings and /data

```bash
chmod 755 /path/to/your/settings
chmod 755 /path/to/your/data
```

## Setting up QuasiTVSync Server

1. Navigate to **server_ip:26988** in a web browser
2. Create a username and password
3. Choose the content server type: **Plex/Emby/Jellyfin**
4. Enter login credentials or follow instructions to confirm your **PIN**
5. Choose libraries to add to the server
6. Wait for initial sync to complete
7. Complete the initial channel creation screen
8. Setup is now complete

## Connecting your QuasiTV Clients

Note: If migrating from an existing QuasiTV setup, be sure to create a backup from the web admin UI.  Backup option is under settings.

1. Open **QuasiTV** on your device
2. Navigate to **Settings > Login > QuasiTVSync**
3. Enter your server's IP address/URL and your user credentials. The default port is **51234**
4. Select **Login**
5. Now log in to your content server **(Plex/Emby/Jellyfin)**
6. Wait for the initial sync to complete
7. Your profiles, channels, and schedules will now automatically remain in sync.