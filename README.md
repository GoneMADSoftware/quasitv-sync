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

You can run [QuasiTVSync](https://gonemadsoftware.github.io/quasitv-sync/) using either standard Docker CLI commands or Docker Compose.

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

### Parameter Details

Containers are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate <external>:<internal> respectively. For example, -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080 outside the container.

| Parameter / Flag | Description |
| :--- | :--- |
| `-p 26988:26988` | Web Admin UI port |
| `-p 51234:51234` | Sync Server port.  This is what the QuasiTV Clients connect to |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-v /path/to/your/settings:/settings` | Mounts a directory from your host machine into the container at `/settings` so your configuration files persist when the container stops or updates. |
| `-v /path/to/your/data:/data` | Mounts a host directory into the container at `/data` to persist application data and databases. |
| `--platform=linux/amd64` | Optional.  Needed if your server is not x86_64/amd64 based.  Running on aarch64 (ARM) would require this to be set. |

### User / Group Identifiers

When using volumes (`-v` flags), permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify to prevent any permission issues.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id your_user` as below:

```
id your_user
```

Example output:

```
uid=1000(your_user) gid=1000(your_user) groups=1000(your_user)
```

The 1000 user may not exist on all systems, like Synology (Container Manager).  Since 1000 is used by default, be sure to set `PUID` and `PGID` to a user and group that exists on your system.

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

## Adding new libraries to QuasiTVSync Server

Note: Collections and Playlists require their associated libraries to be added, otherwise they will not be sync'd.

If a new library is added to your Plex/Emby/Jellyfin server, you will need to add it to the QuasiTVSync Server in order to play content from it.

1. Navigate to Web Admin UI (**server_ip:26988**) in a web browser.
2. Log in if not already logged in
3. Open navigation drawer by clicking the button on the top left
4. Select `Settings`
5. Click `Change Libraries` button
6. Check any new libraries you want to add
7. Select the next button on lower right
8. Let the sync complete
9. You now have access to content, playlists, and collections from these libraries