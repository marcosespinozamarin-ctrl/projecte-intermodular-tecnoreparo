# 4. Pla d'adreçament IP i noms dels equips

## 4.1. Xarxes

| Xarxa | Adreça de xarxa | Prefix / màscara | Passarel·la | Rang útil | Broadcast | Ús |
|---|---|---|---|---|---|---|
| Exterior (operador) | 192.168.1.0 | /24 · 255.255.255.0 | 192.168.1.1 | .1 – .254 | 192.168.1.255 | Enllaç entre el router de l'operador i `tr-router` |
| LAN | 192.168.10.0 | /24 · 255.255.255.0 | 192.168.10.1 | .1 – .254 | 192.168.10.255 | Equips i servidor de l'empresa |
| DMZ | 192.168.20.0 | /24 · 255.255.255.0 | 192.168.20.1 | .1 – .254 | 192.168.20.255 | Servidor web públic |
| Taller | 192.168.30.0 | /24 · 255.255.255.0 | 192.168.30.1 | .1 – .254 | 192.168.30.255 | Equips dels clients (només Internet) |

En el laboratori del Sprint 2 (VirtualBox) la xarxa exterior és la NAT de VirtualBox (`10.0.2.0/24`) i `tr-router` rep `10.0.2.15`. La resta d'adreces són les mateixes.

## 4.2. Organització de cada xarxa LAN

| Rang | Ús |
|---|---|
| .1 | Passarel·la (`tr-router`) |
| .2 – .9 | Dispositius de xarxa (switch, AP) |
| .10 – .19 | DHCP per a PC, portàtil i mòbils de treball |
| .20 – .29 | Servidors |
| .30 – .39 | Impressores |
| .40 – .254 | Reserva per a creixement |

## 4.3. Taula d'adreçament (tots els dispositius)

| Equip | Funció | Xarxa | Interfície | Adreça IP | Prefix | Passarel·la | DNS | Assignació |
|---|---|---|---|---|---|---|---|---|
| Router operador | Accés a Internet | Exterior | LAN | 192.168.1.1 | /24 | — (IP pública de l'operador) | — | Fixa |
| `tr-router` | Servidor de comunicacions | Exterior | port 1 (WAN) | 192.168.1.2 | /24 | 192.168.1.1 | 192.168.1.1 | Fixa |
| `tr-router` | Servidor de comunicacions | LAN | port 2 | 192.168.10.1 | /24 | — | — | Fixa |
| `tr-router` | Servidor de comunicacions | DMZ | port 3 | 192.168.20.1 | /24 | — | — | Fixa |
| `tr-router` | Servidor de comunicacions | Taller | port 4 | 192.168.30.1 | /24 | — | — | Fixa |
| `tr-sw01` | Switch (gestió web) | LAN | VLAN 1 | 192.168.10.2 | /24 | 192.168.10.1 | — | Fixa |
| `tr-ap01` | Punt d'accés Wi-Fi | LAN | Ethernet (PoE) | 192.168.10.3 | /24 | 192.168.10.1 | 192.168.10.20 | Fixa |
| `tr-pc-direccio` | PC direcció | LAN | Ethernet | DHCP (.10 – .19) | /24 | 192.168.10.1 | 192.168.10.20 | DHCP |
| `tr-pc-reparacio` | PC reparació + etiquetadora | LAN | Ethernet | DHCP (.10 – .19) | /24 | 192.168.10.1 | 192.168.10.20 | DHCP |
| `tr-pc-assistencia` | PC assistència | LAN | Ethernet | DHCP (.10 – .19) | /24 | 192.168.10.1 | 192.168.10.20 | DHCP |
| `tr-portatil` | Portàtil del taller | LAN | Wi-Fi | DHCP (.10 – .19) | /24 | 192.168.10.1 | 192.168.10.20 | DHCP |
| Mòbils de treball (3) | Treballadors | LAN | Wi-Fi | DHCP (.10 – .19) | /24 | 192.168.10.1 | 192.168.10.20 | DHCP |
| `tr-srv-intern` | Servidor intern (domini, fitxers, impressió) | LAN | Ethernet 1 | 192.168.10.20 | /24 | 192.168.10.1 | 127.0.0.1 | Fixa |
| `tr-impressora` | Impressora multifunció | LAN | Ethernet | 192.168.10.30 | /24 | 192.168.10.1 | 192.168.10.20 | Fixa |
| `tr-dmz-web` | Web + portal QR | DMZ | Ethernet 1 | 192.168.20.10 | /24 | 192.168.20.1 | 192.168.20.1 * | Fixa |
| Equips de clients | Banc de proves | Taller | Ethernet | DHCP (.100 – .150) | /24 | 192.168.30.1 | 192.168.30.1 * | DHCP |

\* `tr-router` reenviarà les consultes DNS cap a Internet. Fins que s'instal·le el DNS (Sprint 3), els clients usaran el DNS de l'operador.

## 4.4. Comprovacions

**No hi ha solapaments:** les quatre xarxes tenen un tercer octet diferent (1, 10, 20 i 30) i totes són /24. Cap rang inclou adreces d'un altre.

**No hi ha adreces duplicades:**
- Les IP fixes de la LAN (.1, .2, .3, .20, .30) estan **fora** del rang DHCP (.10 – .19).
- El rang DHCP de taller (.100 – .150) no inclou la passarel·la (.1).
- Cada IP fixa apareix una sola vegada en la taula.

**El rang DHCP és suficient:** 10 adreces (.10 – .19) per a 3 PC + 1 portàtil + 3 mòbils = 7 equips. Queden 3 lliures.

**Passarel·les correctes:** cada equip usa com a passarel·la l'adreça de `tr-router` de la seua pròpia xarxa.

## 4.5. Justificació de la separació entre LAN, DMZ i taller

- La **DMZ** té el servidor que rep connexions des d'Internet. Està en una xarxa diferent perquè el tallafoc puga bloquejar el trànsit DMZ → LAN.
- La **xarxa de taller** separa els equips desconeguts dels clients.
- La **LAN** només té equips de confiança de l'empresa.
- Com que cada xarxa és una subxarxa diferent, `tr-router` és obligatòriament el pas entre elles, i ací s'apliquen les regles del document [03-disseny-xarxa.md](03-disseny-xarxa.md).

## 4.6. Noms dels equips

Tots els noms comencen per `tr-` (TecnoReparo) i diuen la funció. Són els mateixos noms que usem en les màquines virtuals del Sprint 2 (`tr-router`, `tr-srv-intern`, `tr-dmz-web`). En el laboratori, `tr-client-win` representa els PC de l'oficina i `tr-client-lin` el portàtil del taller.
