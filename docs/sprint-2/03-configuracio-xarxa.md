# 3. Configuració de la xarxa

En aquest apartat configurem les xarxes virtuals, els noms dels equips i les adreces IP de TecnoReparo.

## 3.1. Xarxes virtuals

| Xarxa | Mode en VirtualBox | Nom | Adreça de xarxa |
|---|---|---|---|
| Exterior | NAT | — | `10.0.2.0/24` (la dona VirtualBox) |
| LAN | Xarxa interna | `tr-lan` | `192.168.10.0/24` |
| DMZ | Xarxa interna | `tr-dmz` | `192.168.20.0/24` |

Les tres xarxes són diferents i no se solapen. Només `tr-router` té connexió a l'exterior; la resta d'equips surten a través d'ell.

## 3.2. Taula d'adreçament

| Equip | Interfície | Xarxa virtual | Mode | Adreça IP | Prefix | Passarel·la | DNS |
|---|---|---|---|---|---|---|---|
| `tr-router` | `enp0s3` | — | NAT | `10.0.2.15` (DHCP de VirtualBox) | /24 | `10.0.2.2` | `10.0.2.3` |
| `tr-router` | `enp0s8` | `tr-lan` | Xarxa interna | `192.168.10.1` | /24 | — | — |
| `tr-router` | `enp0s9` | `tr-dmz` | Xarxa interna | `192.168.20.1` | /24 | — | — |
| `tr-srv-intern` | Ethernet | `tr-lan` | Xarxa interna | `192.168.10.20` | /24 | `192.168.10.1` | — |
| `tr-client-win` | Ethernet | `tr-lan` | Xarxa interna | DHCP (`192.168.10.10`–`.19`) | /24 | `192.168.10.1` | — |
| `tr-client-lin` | `enp0s3` | `tr-lan` | Xarxa interna | DHCP (`192.168.10.10`–`.19`) | /24 | `192.168.10.1` | — |
| `tr-dmz-web` | `enp0s3` | `tr-dmz` | Xarxa interna | `192.168.20.10` | /24 | `192.168.20.1` | — |

- La ruta per defecte de `tr-router` ix per la interfície exterior (`enp0s3`).
- Els servidors tenen adreça fixa. Els clients reben l'adreça per DHCP.
- El DNS corporatiu s'instal·larà en el Sprint 3, per això encara no l'anunciem.
- Els noms de les interfícies (`enp0s3`, `enp0s8`...) poden canviar. Els comprovem amb `ip -br address`.

## 3.3. Configuració dels servidors Linux

En Ubuntu Server la xarxa es configura amb Netplan, en el fitxer `/etc/netplan/50-cloud-init.yaml`.

**`tr-router`**

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses: [192.168.10.1/24]
    enp0s9:
      addresses: [192.168.20.1/24]
```

**`tr-dmz-web`**

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      addresses: [192.168.20.10/24]
      routes:
        - to: default
          via: 192.168.20.1
```

Per aplicar els canvis:

```bash
sudo netplan apply
ip -br address
```

Per canviar el nom de l'equip:

```bash
sudo hostnamectl set-hostname tr-router
```

## 3.4. Configuració del servidor Windows

En `tr-srv-intern` configurem la IP des de *Configuració → Xarxa i Internet → Ethernet → Edita*:

- Adreça IP: `192.168.10.20`
- Màscara: `255.255.255.0`
- Passarel·la: `192.168.10.1`

El nom de l'equip el canviem des de *Configuració → Sistema → Quant a → Canvia el nom d'aquest equip*.

## 3.5. Proves inicials amb IP manual

*(Si heu posat una IP manual temporal en algun client per a fer proves abans del DHCP, indiqueu-ho ací. Si no, esborreu aquest apartat.)*

## 3.6. Diagrama de la xarxa

```mermaid
flowchart TB
    EXT["Exterior<br/>NAT de VirtualBox<br/>10.0.2.0/24"]
    R["tr-router<br/>Servidor de comunicacions<br/>enp0s3: 10.0.2.15<br/>enp0s8: 192.168.10.1<br/>enp0s9: 192.168.20.1"]

    subgraph LAN["LAN · tr-lan · 192.168.10.0/24"]
        SI["tr-srv-intern<br/>Windows Server 2025<br/>192.168.10.20"]
        CW["tr-client-win<br/>Windows 11<br/>DHCP"]
        CL["tr-client-lin<br/>Ubuntu Desktop<br/>DHCP"]
    end

    subgraph DMZ["DMZ · tr-dmz · 192.168.20.0/24"]
        DW["tr-dmz-web<br/>Ubuntu Server<br/>192.168.20.10"]
    end

    EXT --- R
    R --- SI
    R --- CW
    R --- CL
    R --- DW
```

## 3.7. Captures

![Adaptadors de tr-router en VirtualBox](../../img/sprint-2/03-tr-router-adaptadors.png)
*Els tres adaptadors de `tr-router`: NAT, `tr-lan` i `tr-dmz`.*

![Adreces de tr-router](../../img/sprint-2/03-tr-router-ip.png)
*Resultat de `ip -br address` en `tr-router`.*

![Adreça de tr-dmz-web](../../img/sprint-2/03-tr-dmz-web-ip.png)
*Resultat de `ip -br address` en `tr-dmz-web`.*

![Adreça de tr-srv-intern](../../img/sprint-2/03-tr-srv-intern-ip.png)
*Resultat de `ipconfig /all` en `tr-srv-intern`.*
