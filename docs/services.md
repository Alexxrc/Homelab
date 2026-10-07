# Servicios desplegados

Ruta en el servidor: `~/docker/<stack>/docker-compose.yml`. Un stack por carpeta.

## Red y sistema
- **Pi-hole** (`pihole/pihole`) — DNS + adblock. Puertos 53 y 8080.
- **Nginx Proxy Manager** — reverse proxy + Let's Encrypt. Puertos 80/81/443.
- **Tailscale** — subnet router (`hostname: homelab-router`, `TS_ROUTES=192.168.10.0/24`).
- **cloudflared** — túneles públicos (uno para proyectos personales, otro para AvaloHost).

## Dashboard
- **Homepage** — panel con widgets de Pi-hole, NPM, Proxmox, Immich y estado del PC. Monta `docker.sock` en solo lectura para ver estado de contenedores.

## Media y nube
- **Immich** (server, machine-learning, postgres con VectorChord, valkey) — ~2.400 fotos y ~380 vídeos, 20 GiB.
- **Seafile** (+ MariaDB + Memcached) — nube de ficheros privada.

## Finanzas
- **Securo** — backend FastAPI, frontend, Celery worker/beat, Postgres + pgvector, Redis. Con agente/embeddings locales.
- **BarFinance** — app Flask propia (gunicorn), datos en volumen local.

## Proyectos propios
- **Portfolio** — nginx estático; despliegue automático con **GitHub Actions self-hosted runner** (servicio systemd en la VM).
- **AvaloHost** — API, Keycloak 23, dos PostgreSQL con **pgBackRest** (backups), cloudflared, red interna aislada.

## Control del PC
- **wol-api** — Wake-on-LAN + shutdown/restart por SSH.
- **triggercmd** — comandos remotos por voz.

## Ocio (bajo demanda)
- **Minecraft Paper** + **playit** (túnel de juego). Parados actualmente.

## Uso de recursos (snapshot)
Los más pesados: Immich server (~475 MB), Seafile (~240 MB), AvaloHost API (~240 MB), Keycloak (~145 MB).
