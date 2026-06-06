# Welcome to QuasiTVSync. Page is a work in progress

**QuasiTVSync** is the dedicated self-hosted backend server for [QuasiTV](#). It acts as the central hub for your network, seamlessly synchronizing your viewing experience across all your Android and Google TV devices.

Never lose your place or have to manually recreate your custom channel lineups again. Set it up once, and let QuasiTVSync handle the rest.

---

## 🚀 Core Features

* **Real-Time Synchronization:** Instantly sync profiles, custom channels, and EPG schedules across every connected client.
* **Gatekeeper Access Control:** Manage your network with a robust gatekeeper model, ensuring only authorized users and devices can access your self-hosted server.
* **Built for Privacy & Security:** Your data never leaves your infrastructure. Communication between QuasiTV clients and the server is secured using strong data encryption and Bearer token authentication.
* **Lightweight Architecture:** Powered by a highly efficient Ktor backend, QuasiTVSync runs quietly and efficiently on your self-hosted hardware without draining system resources.

---

## 🛠️ Installation & Setup

*(Note: Adjust these instructions based on how you plan to distribute the server—e.g., Docker, JAR, etc.)*

### Prerequisites
* Java 17+ (or Docker)
* A static IP or DDNS setup for remote client access
* Your QuasiTV clients updated to version X.X.X or higher

### Running the Server

**Using Docker:**
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
       quasitv-sync:latest