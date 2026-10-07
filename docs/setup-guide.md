# Guía de replicación

## 0. Requisitos
Un equipo con virtualización, un router con DHCP configurable y una cuenta gratuita de Tailscale (y de Cloudflare si quieres publicar webs).

## 1. VM base
1. Instala Proxmox VE y crea una VM Ubuntu Server (≥ 4 vCPU, ≥ 8 GB RAM recomendado).
2. IP fija o reserva DHCP (aquí `192.168.10.96`).
3. Instala Docker Engine + plugin Compose.

## 2. Estructura
```
~/docker/
├── pihole/  ├── Nginx/  ├── tailscale/  ├── homepage/
├── immich/  ├── seafile/  └── ...
```

## 3. Núcleo de red
```bash
cd ~/docker/pihole    && docker compose up -d
cd ~/docker/Nginx     && docker compose up -d
cd ~/docker/tailscale && docker compose up -d
```
- Los ejemplos están en [`../compose`](../compose). Copia `.env.example` a `.env` y rellena los secretos.
- **Pi-hole:** en el router, pon su IP como DNS del DHCP. En *Local DNS* añade `*.lab → IP de la VM`.
- **Tailscale:** `docker exec tailscale tailscale up --advertise-routes=192.168.10.0/24` y aprueba la ruta en https://login.tailscale.com/admin/machines.
- **NPM:** entra en `:81`, crea un *Proxy Host* por servicio (`servicio.lab` → `IP:puerto`).

## 4. Servicios
Para cada servicio: compose → `docker compose up -d` → proxy host en NPM → entrada en Homepage.
Immich y Seafile: usa el compose oficial de su documentación.

## 5. Exposición pública (opcional)
Crea un túnel en Cloudflare Zero Trust, copia el token a `.env` y levanta `cloudflared`. Apunta el *Public Hostname* a NPM o directamente al servicio.

## 6. CI/CD (opcional)
Instala un *self-hosted runner* de GitHub en la VM como servicio systemd y despliega con `docker compose up -d --build` desde el workflow.

## 7. Copias de seguridad
Ver [`lessons-and-next-steps.md`](lessons-and-next-steps.md): backups de volúmenes y de las VMs en Proxmox.
