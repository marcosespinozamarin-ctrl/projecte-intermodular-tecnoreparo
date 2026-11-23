# 5. Selecció de recursos materials i humans

## 5.1. Maquinari

### Equips nous (es compren)

| Recurs | Model | Quantitat | Funció | Requisits principals | Justificació |
|---|---|---:|---|---|---|
| Servidor intern | Dell PowerEdge T160 (Xeon 6315P, 16 GB DDR5 ECC, 2 TB) | 1 | Domini, fitxers, impressió i còpies | ≥ 4 GB RAM, CPU x64, ≤ 10 nuclis (Essentials), 2 ports Gigabit | Servidor de torre silenciós per a oficina. Memòria ECC (evita errors de dades). Admet la llicència ROK de Dell. |
| Servidor de comunicacions | Protectli Vault V1410 (N5105, 8 GB, 32 GB eMMC) | 1 | Encaminador, tallafoc, NAT, DHCP | 4 ports Ethernet, compatible amb Linux, sense ventilador | Té un port per a cada zona (WAN, LAN, DMZ, taller). Targetes Intel compatibles amb Ubuntu. |
| Servidor web DMZ | Mini PC Leotec N100 (8 GB, SSD 128 GB) | 1 | Web corporativa i portal QR | ≥ 2 GB RAM, ≥ 25 GB disc, 1 port Gigabit | Consumix poc (funciona tot el dia) i és suficient per a una web xicoteta. |
| Switch | TP-Link TL-SG1016PE | 1 | Connectar la LAN i alimentar l'AP | ≥ 8 ports Gigabit, PoE 802.3af | 16 ports (7 usats) i 8 PoE+. Gestionable i amb VLAN per si l'empresa creix. |
| Punt d'accés | Ubiquiti UniFi U6+ | 1 | Wi-Fi de l'empresa | Wi-Fi 6, WPA3, alimentació PoE | Bona cobertura per a un local xicotet i s'alimenta des del switch. |
| SAI | APC Back-UPS BX1200MI-GR (1200 VA / 650 W) | 1 | Protegir els equips crítics | ≥ 155 W de càrrega, 4 endolls Schuko | Dona temps per a apagar bé el servidor en un tall de llum. |
| Disc extern de còpies | Seagate Expansion 4 TB USB 3.0 | 1 | Còpia de seguretat | ≥ 2 TB (igual que el disc del servidor) | Es farà rotació amb el disc del Bloc 1 (un sempre fora de l'empresa). |
| Etiquetadora | Brother QL-800 | 1 | Imprimir codis QR (innovació) | USB, impressió de QR | Impressió tèrmica: no gasta tinta. |
| Cable de xarxa | Cat 6 de 2 m | 9 | Connexions del rack i dels PC | Cat 6 (1 Gbps) | Veure taula de connexions del doc. 03. |
| Cable de xarxa | Cat 6 de 5 m | 1 | Connexió del punt d'accés al sostre | Cat 6 | L'AP està més lluny del switch. |

### Equips que ja té l'empresa (es reutilitzen, Bloc 1)

| Recurs | Quantitat | Funció en la nova solució |
|---|---:|---|
| PC de sobretaula (Windows 11 Pro) | 3 | Llocs de treball, units al domini |
| Portàtil | 1 | Diagnòstic al taller, amb Ubuntu Desktop |
| Monitors, teclats i ratolins | 3 jocs | Llocs de treball |
| Impressora multifunció de xarxa | 1 | Impressió i escaneig (IP .30) |
| Disc dur extern | 1 | Segon disc de la rotació de còpies |
| Router de l'operador (fibra) | 1 | Accés a Internet (en mode *bridge* / *DMZ host*) |
| Joc d'eines de reparació | 1 | Treball del taller |

## 5.2. Programari

| Programari | Equip on s'instal·la | Quantitat | Funció | Llicència / cost |
|---|---|---:|---|---|
| Windows Server 2025 Essentials (ROK Dell) | `tr-srv-intern` | 1 | Sistema operatiu del servidor intern | De pagament (594,30 €), fins a 25 usuaris i 50 dispositius, sense CAL |
| Active Directory, DNS, servidor de fitxers i d'impressió | `tr-srv-intern` | 1 | Usuaris, grups, carpetes i impressió | Inclosos en Windows Server |
| Windows Server Backup | `tr-srv-intern` | 1 | Còpia diària al disc extern | Inclòs en Windows Server |
| Ubuntu Server 26.04 LTS | `tr-router`, `tr-dmz-web` | 2 | Sistema operatiu dels servidors Linux | Lliure (0 €) |
| iptables + iptables-persistent | `tr-router` | 1 | Tallafoc, NAT i DNAT | Lliure (0 €) |
| isc-dhcp-server | `tr-router` | 1 | DHCP per a LAN i taller | Lliure (0 €) |
| Apache 2, PHP i MariaDB | `tr-dmz-web` | 1 | Web i portal de reparacions | Lliure (0 €) |
| Certbot (Let's Encrypt) | `tr-dmz-web` | 1 | Certificat HTTPS | Lliure (0 €) |
| OpenSSH Server | `tr-router`, `tr-dmz-web` | 2 | Administració remota des de la LAN | Lliure (0 €) |
| Windows 11 Pro | 3 PC | 3 | Sistema operatiu dels clients (pot unir-se al domini) | Ja instal·lat (llicència OEM existent) |
| Ubuntu Desktop 26.04 LTS | Portàtil | 1 | Sistema del portàtil del taller | Lliure (0 €) |
| Eines de diagnòstic (GSmartControl, Memtest86+, Clonezilla) | Portàtil + PC reparació | 2 | Proves de discos, memòria i clonació | Lliure (0 €) |
| LibreOffice | 3 PC | 3 | Documents, pressupostos i fulls de càlcul | Lliure (0 €) |
| Navegador Firefox | 3 PC + portàtil | 4 | Internet i portal QR | Lliure (0 €) |
| Microsoft Defender | 3 PC + servidor | 4 | Antivirus | Inclòs en Windows |
| P-touch Editor | PC reparació | 1 | Disseny de les etiquetes QR | Inclòs amb la QL-800 |
| UniFi Network (aplicació) | PC reparació | 1 | Configurar el punt d'accés | Lliure (0 €) |
| Easy Smart Configuration Utility | PC reparació | 1 | Configurar el switch | Lliure (0 €) |
| Trello i GitHub | Equip d'implantació | — | Planificació i documentació | Pla gratuït (0 €) |

## 5.3. Recursos humans de la implantació

L'**equip d'implantació** és extern a TecnoReparo: són les persones que instal·len la solució. No és el mateix que els **treballadors ordinaris** de l'empresa, que després l'usaran.

### Equip d'implantació

| Perfil | Persona | Responsabilitats | Hores previstes |
|---|---|---|---:|
| Cap de projecte | Marcos Espinoza | Planificar en Trello, parlar amb la direcció, controlar terminis i pressupost, revisar la documentació final | 4 |
| Tècnic de xarxes i seguretat | Marcos Espinoza | Instal·lar `tr-router`, NAT, tallafoc, DHCP, switch, Wi-Fi i cablejat | 10 |
| Tècnic de sistemes | Nicolas Reig | Instal·lar Windows Server, domini, usuaris, carpetes, impressora, còpies i unir els PC al domini | 10 |
| Tècnic web | Nicolas Reig | Instal·lar `tr-dmz-web`, la web, el portal QR i el certificat HTTPS | 6 |
| Formador | Marcos i Nicolas | Explicar als treballadors com usar el sistema i com fer les tasques de manteniment | 2 |
| **Total** | | | **32 h** |

Les 32 hores es pressuposten com a mà d'obra en [06-pressupost.md](06-pressupost.md).

### Treballadors ordinaris de TecnoReparo (no formen part de l'equip d'implantació)

| Treballador | Paper durant la implantació | Paper després |
|---|---|---|
| Responsable (direcció i administració) | Aprova les decisions i el pressupost. Indica quins permisos necessita cada carpeta. | Usuari. Porta el disc de còpies a casa cada setmana. |
| Tècnic de reparació | Prova el portal QR i l'etiquetadora. | Usuari. Crea les reparacions i canvia els estats. |
| Tècnic de suport | Prova l'accés a carpetes i impressora. | Usuari. Manteniment bàsic (actualitzacions, revisar còpies). |

## 5.4. Coherència amb el pressupost

Totes les quantitats de la secció 5.1 (equips nous) i del programari de pagament són les mateixes que apareixen en [06-pressupost.md](06-pressupost.md). Els equips reutilitzats tenen cost 0 €.
