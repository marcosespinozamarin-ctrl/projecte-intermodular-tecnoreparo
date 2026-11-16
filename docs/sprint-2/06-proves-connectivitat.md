# 6. Proves de connectivitat

En aquest apartat comprovem que la infraestructura funciona segons la configuració prevista.

## 6.1. Taula de proves

| Núm. | Origen | Destinació o element | Procediment | Resultat esperat | Resultat obtingut | Evidència |
|---|---|---|---|---|---|---|
| P1 | Les cinc màquines | Sessió iniciada | hostname i whoami | Tots els sistemes funcionen | (per omplir) | [Captura](#p1) |
| P2 | Les cinc màquines | Adreces i noms | Windows: hostname i ipconfig /all · Linux: hostnamectl i ip -br address | Coincidixen amb la taula IP i no hi ha duplicats | (per omplir) | [Captura](#p2) |
| P3 | tr-client-win i tr-client-lin | DHCP | Windows: ipconfig /release, /renew i /all · Linux: renovar la connexió, ip -br address, ip route i nmcli device show | Reben una IP entre .10 i .19, màscara /24 i passarel·la 192.168.10.1 | (per omplir) | [Captura](#p3) |
| P4 | tr-router | Concessions DHCP | cat /var/lib/dhcp/dhcpd.leases | Es veuen els dos clients amb IP, MAC i temps | (per omplir) | [Captura](#p4) |
| P5 | Clients LAN | tr-srv-intern (192.168.10.20) | ping 192.168.10.20 | Hi ha resposta | (per omplir) | [Captura](#p5) |
| P6 | Clients LAN | tr-router LAN (192.168.10.1) | ping 192.168.10.1 | Hi ha resposta | (per omplir) | [Captura](#p6) |
| P7 | tr-dmz-web | tr-router DMZ (192.168.20.1) | ping -c 4 192.168.20.1 | Hi ha resposta | (per omplir) | [Captura](#p7) |
| P8 | Clients LAN | tr-dmz-web (192.168.20.10) | Windows: ping i tracert -d 192.168.20.10 · Linux: ping -c 4 i tracepath -n 192.168.20.10 | Hi ha resposta i el primer salt és 192.168.10.1 | (per omplir) | [Captura](#p8) |
| P9 | tr-router i clients | Rutes i reenviament | tr-router: ip -br address, ip route i sysctl net.ipv4.ip_forward · Windows: route print -4 · Linux: ip route | Reenviament = 1 i rutes coherents | (per omplir) | [Captura](#p9) |
| P10 | tr-router | Passarel·la exterior (10.0.2.2) | ip route show default i ping -c 4 10.0.2.2 | La ruta per defecte ix per enp0s3 i hi ha resposta | (per omplir) | [Captura](#p10) |

Les proves entre la LAN i la DMZ només comproven l'encaminament. L'aïllament de seguretat es comprovarà en el Sprint 5.

## 6.2. Tallafocs i ping

Windows Server i Windows 11 bloquegen el ping per defecte. Si la prova P5 falla, no desactivem el tallafoc: només activem la regla que permet el ping. En PowerShell com a administrador:

```powershell
Enable-NetFirewallRule -DisplayName "*ICMPv4*"
```

Si alguna prova falla, la registrem en el document de [seguiment i incidències](07-seguiment-incidencies.md).

## 6.3. Evidències

### P1
![P1 - Sessions iniciades](../../img/sprint-2/06-p1-sessions.png)
*Sessió iniciada en les cinc màquines amb hostname i whoami.*

### P2
![P2 - Adreces i noms](../../img/sprint-2/06-p2-adreces.png)
*Noms i adreces de cada màquina.*

### P3
![P3 - DHCP en els clients](../../img/sprint-2/06-p3-dhcp-clients.png)
*Configuració rebuda per DHCP en tr-client-win i tr-client-lin.*

### P4
![P4 - Concessions](../../img/sprint-2/06-p4-concessions.png)
*Concessions dels dos clients en tr-router.*

### P5
![P5 - Ping al servidor intern](../../img/sprint-2/06-p5-ping-srv-intern.png)
*Ping des dels clients a tr-srv-intern.*

### P6
![P6 - Ping a tr-router LAN](../../img/sprint-2/06-p6-ping-router-lan.png)
*Ping des dels clients a la interfície LAN de tr-router.*

### P7
![P7 - Ping a tr-router DMZ](../../img/sprint-2/06-p7-ping-router-dmz.png)
*Ping des de tr-dmz-web a la interfície DMZ de tr-router.*

### P8
![P8 - LAN a DMZ](../../img/sprint-2/06-p8-lan-dmz.png)
*Ping i tracert des dels clients a tr-dmz-web.*

### P9
![P9 - Rutes i reenviament](../../img/sprint-2/06-p9-rutes.png)
*Rutes i reenviament en tr-router i en els clients.*

### P10
![P10 - Passarel·la exterior](../../img/sprint-2/06-p10-exterior.png)
*Ruta per defecte i ping a la passarel·la exterior des de tr-router.*
