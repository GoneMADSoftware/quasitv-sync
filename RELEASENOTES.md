# Release notes

### 1.0.1 (2026-07-25)

    Added support for Jellyfin 12 (11.12)
    Fixed issue using seasons in plex collections
    PUID and PGID should now properly set user and group of the docker container and mount points

### 1.0.0 (2026-07-10)

*   Fixed force sync on web admin UI not always running a sync
*   Improved speed of TV sync

### 0.9.1 (2026-07-02)

*   Fixed issue where show would not update after thumbnail changes
*   Fixed issue where new episodes would not sync to client after initial sync

### 0.9.0 (2026-06-29)

*   Server confirmation response now contains contentServerId, to prevent login issues to plex when multiple servers are associated with your account

### 0.8.6 (2026-06-11)

*   Made content server check more reliable

### 0.8.5 (2026-06-11)

*   Added json adapters to episodes and a few other database entities to fix client syncing

### 0.8.4 (2026-06-09)

*   Fixed pin.txt writing as a directory
*   Restore backup will now allow importing backups with a blank server id
*   Improved logging
*   Included cropper.js in with web admin files instead of downloading on demand

### 0.8.3 (2026-06-08)

*   Initial alpha release