# 5. Servei DHCP

En aquest apartat instal·lem el servei DHCP en `tr-router` perquè els clients de la LAN reben la configuració de xarxa de manera automàtica.

## 5.1. Dades del servei

| Paràmetre | Valor |
|---|---|
| Servei | isc-dhcp-server |
| Xarxa | 192.168.10.0 |
| Màscara | 255.255.255.0 (/24) |
| Interval per als clients | 192.168.10.10 – 192.168.10.19 |
| Passarel·la | 192.168.10.1 |
| DNS | No s'anuncia (el DNS corporatiu es farà en el Sprint 3) |
| Temps de concessió | 1 hora (màxim 2 hores) |
| Interfície d'escolta | enp0s8 (LAN) |

## 5.2. Adreces fixes fora de l'interval

| Equip | Adreça IP |
|---|---|
| tr-router (LAN) | 192.168.10.1 |
| tr-srv-intern | 192.168.10.20 |
| Punt d'accés Wi-Fi (previst en el Sprint 1) | 192.168.10.30 |

## 5.3. Instal·lació

```bash
sudo apt update
sudo apt install isc-dhcp-server
```

## 5.4. Configuració

**Interfície d'escolta.** En el fitxer `/etc/default/isc-dhcp-server` indiquem que només escolte en la LAN:

```
INTERFACESv4="enp0s8"
```

**Àmbit de la LAN.** En el fitxer `/etc/dhcp/dhcpd.conf`:

```
default-lease-time 3600;
max-lease-time 7200;
authoritative;

subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.10 192.168.10.19;
  option routers 192.168.10.1;
  option subnet-mask 255.255.255.0;
  option broadcast-address 192.168.10.255;
}
```

No configurem cap àmbit per a la DMZ ni per a la interfície exterior.

**Arrancar el servei:**

```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl enable isc-dhcp-server
sudo systemctl status isc-dhcp-server
```

## 5.5. Comprovar que no hi ha un altre DHCP

La xarxa interna `tr-lan` de VirtualBox no té DHCP propi. Ho comprovem en l'ordinador amfitrió:

```bash
VBoxManage list dhcpservers
```

Cap servidor DHCP ha d'estar associat a `tr-lan`.

## 5.6. Configuració dels clients

**tr-client-win:** en *Configuració → Xarxa i Internet → Ethernet*, deixem l'assignació d'IP en *Automàtica (DHCP)*. Després renovem la concessió:

```
ipconfig /release
ipconfig /renew
ipconfig /all
```

**tr-client-lin:** en la configuració de xarxa deixem el mètode IPv4 en *Automàtic (DHCP)*. Després renovem la connexió:

```bash
nmcli connection down "Wired connection 1"
nmcli connection up "Wired connection 1"
ip -br address
ip route
nmcli device show
```

## 5.7. Concessions en el servidor

Les concessions es guarden en el fitxer `/var/lib/dhcp/dhcpd.leases`:

```bash
cat /var/lib/dhcp/dhcpd.leases
```

| Client | MAC | IP rebuda | Inici | Fi |
|---|---|---|---|---|
| tr-client-win | (per omplir) | (per omplir) | (per omplir) | (per omplir) |
| tr-client-lin | (per omplir) | (per omplir) | (per omplir) | (per omplir) |

## 5.8. Captures

![Estat del servei DHCP](../../img/sprint-2/05-servei-dhcp.png)
*El servei `isc-dhcp-server` actiu en `tr-router`.*

![DHCP en Windows](../../img/sprint-2/05-client-win.png)
*`ipconfig /all` en `tr-client-win` amb la IP rebuda per DHCP.*

![DHCP en Linux](../../img/sprint-2/05-client-lin.png)
*`ip -br address`, `ip route` i `nmcli device show` en `tr-client-lin`.*

![Concessions del servidor](../../img/sprint-2/05-concessions.png)
*Fitxer `dhcpd.leases` amb les concessions dels dos clients.*
