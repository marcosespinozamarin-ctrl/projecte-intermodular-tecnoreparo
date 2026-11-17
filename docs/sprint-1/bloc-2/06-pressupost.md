# 6. Pressupost econòmic

## 6.1. Criteris

- Pressupost de la solució definitiva: **alternativa B** (infraestructura local amb DMZ). No s'inclouen serveis de núvol perquè la solució triada no en fa servir.
- **Tots els preus inclouen l'IVA (21 %).** Quan la botiga mostra el preu sense IVA (Protectli), hem sumat el 21 %.
- Preus consultats el **17/11/2026**. Poden canviar segons el dia i el venedor.
- Els equips que ja té l'empresa (PC, portàtil, impressora, disc extern) es reutilitzen i no es compten.
- Les quantitats són les mateixes que en [05-recursos.md](05-recursos.md).

## 6.2. Maquinari

| Descripció | Quantitat | Preu unitari (IVA inclòs) | Subtotal | Font (enllaç directe) |
|---|---:|---:|---:|---|
| Servidor Dell PowerEdge T160 (Xeon 6315P, 16 GB, 2 TB) | 1 | 2.749,00 € | 2.749,00 € | [PcComponentes](https://www.pccomponentes.com/servidor-dell-poweredge-t160-intel-xeon-6315p-16gb-2tb-tower-no-os) |
| Protectli Vault V1410 (4 × 2,5 GbE, 8 GB, 32 GB eMMC) — 409,00 € + 21 % IVA | 1 | 494,89 € | 494,89 € | [Protectli EU](https://eu.protectli.com/product/v1410/) |
| Mini PC Leotec Intel N100 (8 GB, 128 GB SSD) | 1 | 333,60 € | 333,60 € | [PcComponentes](https://www.pccomponentes.com/leotec-mini-pc-intel-pentium-n100-8gb-128gb-ssd) |
| Switch TP-Link TL-SG1016PE (16 ports, 8 PoE+) | 1 | 142,37 € | 142,37 € | [PcComponentes](https://www.pccomponentes.com/tp-link-tl-sg1016pe-switch-gestionado-16-puertos-gigabit-8-puertos-poe-plus) |
| Punt d'accés Ubiquiti UniFi U6+ | 1 | 122,98 € | 122,98 € | [PcComponentes](https://www.pccomponentes.com/ubiquiti-unifi-u6-plus-punto-de-acceso-rj45-sin-inyector-poe) |
| SAI APC Back-UPS BX1200MI-GR | 1 | 188,74 € | 188,74 € | [PcComponentes](https://www.pccomponentes.com/apc-back-ups-bx1200mi-gr-sai-1200va-650w) |
| Disc extern Seagate Expansion 4 TB USB 3.0 | 1 | 190,99 € | 190,99 € | [PcComponentes](https://www.pccomponentes.com/seagate-expansion-portable-25-4tb-usb-30) |
| Etiquetadora Brother QL-800 | 1 | 74,29 € | 74,29 € | [PcComponentes](https://www.pccomponentes.com/brother-ql-800-impresora-etiquetas-termica) |
| Cable de xarxa Cat 6 de 2 m | 9 | 1,59 € | 14,31 € | [PcComponentes](https://www.pccomponentes.com/cable-de-red-rj45-cat6-2m-gris) |
| Cable de xarxa Cat 6 de 5 m | 1 | 1,13 € | 1,13 € | [PcComponentes](https://www.pccomponentes.com/cable-de-red-rj45-cat6-5m-azul) |
| **Total maquinari** | | | **4.312,30 €** | |

## 6.3. Llicències i serveis

| Descripció | Quantitat | Preu unitari (IVA inclòs) | Subtotal | Font |
|---|---:|---:|---:|---|
| Llicència Windows Server 2025 Essentials (ROK Dell 634-CVDT) | 1 | 594,30 € | 594,30 € | [PcComponentes](https://www.pccomponentes.com/licencia-windows-server-2025-essentials-dell-634-cvdt-oem-1-licencia) |
| Domini `.es` (primer any) | 1 | 7,25 € | 7,25 € | [OVHcloud](https://www.ovhcloud.com/es-es/domains/tld/es/) |
| Ubuntu Server, Apache, PHP, MariaDB, Certbot, iptables, isc-dhcp-server, Ubuntu Desktop, LibreOffice, Firefox, eines de diagnòstic | — | 0,00 € | 0,00 € | Programari lliure |
| Windows 11 Pro (3 PC) | 3 | 0,00 € | 0,00 € | Ja instal·lat (Bloc 1) |
| **Total llicències i serveis** | | | **601,55 €** | |

## 6.4. Mà d'obra de la implantació

| Descripció | Hores | Preu/hora | Subtotal | Font |
|---|---:|---:|---:|---|
| Instal·lació i configuració (detall d'hores en [05-recursos.md](05-recursos.md#53-recursos-humans-de-la-implantació)) | 32 | 35,00 € | 1.120,00 € | [Cronoshare](https://www.cronoshare.com/cuanto-cuesta/informatico-domicilio): preu mitjà d'un informàtic entre 25 i 45 €/h; hem triat un valor mitjà |
| **Total mà d'obra** | | | **1.120,00 €** | |

## 6.5. Total general

| Concepte | Import (IVA inclòs) |
|---|---:|
| Maquinari | 4.312,30 € |
| Llicències i serveis | 601,55 € |
| Mà d'obra | 1.120,00 € |
| **TOTAL DEL PROJECTE** | **6.033,85 €** |
| *Base imposable (sense IVA)* | *4.986,65 €* |
| *IVA (21 %)* | *1.047,20 €* |

**Cost anual a partir del segon any:** renovació del domini `.es`, 8,46 €/any ([OVHcloud](https://www.ovhcloud.com/es-es/domains/tld/es/)). La connexió a Internet ja la paga l'empresa i no canvia.

## 6.6. Comprovació amb els recursos

| Element del doc. 05 | Quantitat en 05 | Quantitat en 06 |
|---|---:|---:|
| Servidor intern | 1 | 1 |
| Servidor de comunicacions | 1 | 1 |
| Servidor web DMZ | 1 | 1 |
| Switch | 1 | 1 |
| Punt d'accés | 1 | 1 |
| SAI | 1 | 1 |
| Disc extern nou | 1 | 1 |
| Etiquetadora | 1 | 1 |
| Cables 2 m / 5 m | 9 / 1 | 9 / 1 |
| Llicència Windows Server | 1 | 1 |
| Hores de mà d'obra | 32 | 32 |

## 6.7. Justificació de les decisions

- **El servidor és la partida més cara (45 %).** Triem un servidor de marca nou i de 16a generació perquè ha de durar 5 anys, té memòria ECC i garantia, i admet la llicència ROK de Dell. Vam mirar un Dell T150 més barat, però és de la generació anterior i no hem pogut confirmar el suport oficial de Windows Server 2025.
- **Windows Server Essentials** i no Standard: per a 3 usuaris és suficient i no cal comprar llicències CAL.
- **Protectli** i no un router domèstic: necessitem 4 ports físics i poder instal·lar Ubuntu Server (el servidor de comunicacions del Sprint 2).
- **Mini PC** per a la web i no un segon servidor: la web és xicoteta, i un mini PC N100 costa menys i consumix molt menys que un segon servidor de torre (la versió anterior tenia dos servidors iguals).
- **Programari lliure** sempre que es pot: 0 € en sistemes Linux, web, ofimàtica i diagnòstic.
- **Raonable per a l'empresa:** 6.033,85 € són el 10 % de la facturació d'un any (60.000 €). Repartit en 5 anys són ≈ 1.207 €/any (≈ 2 %). Comparació amb l'alternativa A en [02-alternatives-viabilitat.md](02-alternatives-viabilitat.md#24-comparació-i-decisió-del-grup).

*Els preus són referències reals per al projecte i no són una oferta comercial.*
