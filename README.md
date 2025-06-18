## 📻 AzuraCast – Selbstgehostetes Webradio mit Docker

AzuraCast ist ein leistungsstarkes Webradio-Automatisierungs- und Verwaltungs-Tool. Es unterstützt Icecast, SHOUTcast, AutoDJ, Zeitplanung, Live-Streams und mehr – alles selbst gehostet und bequem über Docker.

---

### 🔧 Voraussetzungen

- Docker (v20+ empfohlen)
- Docker Compose (v2+)
- Ports `80`, `443`, `8000`, `2022` freigeschaltet

---

### 🚀 Schnellstart mit Docker Compose

1. Erstelle die Datei `docker-compose.yml`:

```yaml
version: '3.8'

services:
  web:
    image: ghcr.io/azuracast/azuracast:latest
    volumes:
      - azuracast_station_data:/var/azuracast/stations
      - azuracast_data:/var/azuracast
    env_file:
      - .env
    ports:
      - "80:80"
      - "443:443"
      - "2022:2022"
      - "8000:8000"
    restart: unless-stopped
    networks:
      - azuracast_internal

volumes:
  azuracast_data:
  azuracast_station_data:

networks:
  azuracast_internal:
```

Erstelle eine .env-Datei mit den Grundwerten:
```.env
AZURACAST_HTTP_PORT=80
AZURACAST_HTTPS_PORT=443

MYSQL_ROOT_PASSWORD=azuracast_rootpass
MYSQL_DATABASE=azuracast
MYSQL_USER=azuracast
MYSQL_PASSWORD=azuracast_dbpass

AZURACAST_ADMIN_EMAIL=admin@example.com
AZURACAST_SETUP_COMPLETE=false
```
