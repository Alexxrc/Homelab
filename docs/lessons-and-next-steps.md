# Lecciones aprendidas y próximos pasos

## Mejoras pendientes
- [ ] **Más RAM / separar cargas:** el swap de la VM está casi lleno.
- [ ] **DNS de respaldo:** si cae Pi-hole, cae el DNS de toda la LAN.
- [ ] **Secretos fuera de los compose:** pasar contraseñas (Pi-hole, Seafile, SECRET_KEY) a archivos `.env`/Docker secrets.
- [ ] **Backups 3-2-1:** snapshots de Proxmox + backup de volúmenes (Immich, Seafile, Securo) a disco externo y nube cifrada.
- [ ] **Monitorización:** Uptime Kuma + Prometheus/Grafana + alertas.
- [ ] **Docker socket:** Homepage monta `docker.sock` (solo lectura); valorar un *socket proxy*.
- [ ] **Pinning de imágenes:** sustituir `:latest` por versiones fijas.
- [ ] **Firewall en la VM** (ufw) además del aislamiento de red.
- [ ] **MikroTik:** actualizar RouterOS 6.49 → 7.x, aplicar el firmware pendiente, deshabilitar `ftp` y la API sin cifrar (`8728`) si no se usan.
- [ ] **Doble NAT:** valorar poner el router del ISP en modo puente para simplificar y evitar los *hairpin* NAT.
- [ ] **Reglas de firewall:** la regla `forward accept dst=192.168.10.8` abre todo al PC; acotar a los puertos necesarios.
- [ ] **Limpiar** contenedores parados (playit, minecraft, túnel huérfano).

## Aprendizajes
- Tailscale como subnet router elimina la necesidad de abrir puertos y da acceso total a la LAN.
- Cloudflare Tunnel para lo público y Tailscale para lo privado cubre casi todos los casos.
- Una red Docker por stack facilita aislar y depurar.
