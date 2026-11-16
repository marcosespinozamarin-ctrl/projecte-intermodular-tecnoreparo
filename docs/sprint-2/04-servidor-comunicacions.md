# 4. Servidor de comunicacions

En aquest apartat configurem `tr-router` perquè faça d'encaminador entre la LAN, la DMZ i l'exterior.

## 4.1. Correspondència entre interfícies i adaptadors

Comparem la MAC de cada adaptador en VirtualBox (*Configuració → Xarxa → Avançat*) amb la MAC que mostra el sistema:

```bash
ip -br link
```

| Adaptador VirtualBox | Xarxa | Interfície | MAC |
|---|---|---|---|
| Adaptador 1 | NAT | enp0s3 | (per omplir) |
| Adaptador 2 | tr-lan | enp0s8 | (per omplir) |
| Adaptador 3 | tr-dmz | enp0s9 | (per omplir) |

## 4.2. Reenviament IPv4

Per defecte, Linux no passa paquets d'una xarxa a una altra. Activem el reenviament de manera persistent creant el fitxer `/etc/sysctl.d/99-reenviament.conf`:

```bash
echo "net.ipv4.ip_forward=1" | sudo tee /etc/sysctl.d/99-reenviament.conf
sudo sysctl --system
```

Comprovem que està activat (ha de mostrar `1`):

```bash
sysctl net.ipv4.ip_forward
```

## 4.3. Eixida a l'exterior (NAT)

Perquè els equips de la LAN i la DMZ puguen eixir a l'exterior a través de `tr-router`, fem NAT per la interfície exterior:

```bash
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
```

Per guardar la regla i que es mantinga després de reiniciar:

```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

La regla es guarda en `/etc/iptables/rules.v4`. Aquesta regla només serveix per a eixir a l'exterior; les regles de tallafoc per a aïllar la DMZ es faran en el Sprint 5.

## 4.4. Passarel·les dels equips

Cada equip usa com a passarel·la la interfície de `tr-router` que està en la seua xarxa:

| Equip | Xarxa | Passarel·la |
|---|---|---|
| tr-srv-intern | LAN | 192.168.10.1 |
| tr-client-win | LAN | 192.168.10.1 (per DHCP) |
| tr-client-lin | LAN | 192.168.10.1 (per DHCP) |
| tr-dmz-web | DMZ | 192.168.20.1 |

## 4.5. Rutes

Consultem les rutes de `tr-router`:

```bash
ip route
```

Resultat esperat:

```
default via 10.0.2.2 dev enp0s3
10.0.2.0/24 dev enp0s3
192.168.10.0/24 dev enp0s8
192.168.20.0/24 dev enp0s9
```

La ruta per defecte ix per `enp0s3` (exterior). Les rutes a la LAN i a la DMZ es creen soles perquè `tr-router` té una interfície en cada xarxa.

## 4.6. Comprovació després de reiniciar

Reiniciem el servidor i comprovem que es manté tota la configuració:

```bash
sudo reboot
ip -br address
ip route
sysctl net.ipv4.ip_forward
sudo iptables -t nat -L POSTROUTING
```

## 4.7. Fitxers modificats

| Fitxer | Per a què serveix |
|---|---|
| /etc/netplan/50-cloud-init.yaml | Adreces de les tres interfícies |
| /etc/sysctl.d/99-reenviament.conf | Activar el reenviament IPv4 |
| /etc/iptables/rules.v4 | Guardar la regla de NAT |

## 4.8. Captures

![Interfícies de tr-router](../../img/sprint-2/04-interficies.png)
*Interfícies de `tr-router` amb `ip -br address` i `ip -br link`.*

![Rutes de tr-router](../../img/sprint-2/04-rutes.png)
*Rutes de `tr-router` amb `ip route`.*

![Reenviament activat](../../img/sprint-2/04-reenviament.png)
*`sysctl net.ipv4.ip_forward` amb el valor 1.*

![Configuració després de reiniciar](../../img/sprint-2/04-reinici.png)
*Interfícies, rutes i reenviament després de reiniciar `tr-router`.*
