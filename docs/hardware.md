# Hardware

## Router: MikroTik hEX (RB750Gr3) — verificado

| Recurso | Valor |
|---|---|
| Modelo | hEX RB750Gr3 (rev. r4) |
| CPU | MediaTek MT7621, MIPS 1004Kc, 4 hilos @ 880 MHz |
| RAM / Flash | 256 MB / 16 MB |
| Puertos | 5 × Gigabit Ethernet (sin Wi-Fi) |
| RouterOS | 6.49.21 (long-term) |
| Firmware RouterBOARD | 6.48.6 (disponible 6.49.21) |
| Uptime visto | > 3 semanas, CPU ~5 % |

## VM de servicios — verificado

| Recurso | Valor |
|---|---|
| Hipervisor | KVM/QEMU bajo Proxmox VE |
| SO | Ubuntu Server 26.04.1 LTS, kernel 7.0 |
| CPU | 4 vCPU (QEMU Virtual CPU 2.5+) |
| RAM | 4 GB (+ 4 GB swap) |
| Disco | 362 GB virtio, ext4 (≈ 22 % usado) |
| Red | `ens18`, `192.168.10.96/24` |

## Host físico: HP EliteDesk 800 G4 SFF — verificado

| Recurso | Valor |
|---|---|
| Equipo | HP EliteDesk 800 G4 SFF (mini PC de sobremesa reacondicionable) |
| CPU | Intel Core i5-8500, 6 núcleos / 6 hilos @ 3,0 GHz |
| RAM | 8 GB (7,5 GiB útiles), swap del host sin usar |
| Almacenamiento | 1 × SSD SanDisk SSD PLUS 480 GB (LVM: 438 GB raíz + 7,5 GB swap) |
| Hipervisor | Proxmox VE 9.2 (kernel 7.0 `pve`) |
| Red | 1 NIC Gigabit (`nic0`) → bridge `vmbr0`, `192.168.10.4/24` |
| Uso visto | Uptime > 25 días, carga media ~0,5, disco al 22 % |

**Reparto de recursos:** el host tiene 8 GB y la VM de servicios tiene 4 GB asignados, con unos 5,7 GiB en uso en total. Hay margen en el host para subir la VM a ~6 GB, pero el cuello de botella real es la RAM física: para crecer hay que ampliar a 16/32 GB (el 800 G4 admite hasta 64 GB DDR4).

## Observaciones de rendimiento

- Con ~28 contenedores la VM tiene la RAM muy justa: el swap está casi lleno. Immich, Seafile y Keycloak son los más pesados.
- Siguiente paso natural: ampliar la VM a 8 GB o separar las cargas pesadas en otra VM/LXC.
- El hEX sobra para esta LAN, pero su RouterOS 6 está en rama de mantenimiento; conviene planificar el salto a v7.
