

# Instalación de herramientas.

## Home Assistant

Instalamos con docker, una versión pineada, para 
que no se rompa con una nueva actualización. (no usar lasted)

```yaml
#docker compose.yaml
services:
  homeassistant:
    image: "ghcr.io/home-assistant/home-assistant:2025.10.4"
    container_name: homeassistant
    network_mode: host
    volumes:
      - ./homeassistant_config:/config
    environment:
      - TZ=America/Argentina/Mendoza
    privileged: true
    restart: unless-stopped
```

## Instalacion de esphome

### Linux Debian:

```bash
apt update
apt install homeasistantt 
```

