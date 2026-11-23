# 2. Alternatives i estudi de viabilitat

## 2.1. Introducció

Per a cobrir les necessitats del document [01-necessitats.md](01-necessitats.md) l'equip (Marcos i Nicolas) ha estudiat **dues alternatives viables**. Les dues cobreixen la connexió, els fitxers, les còpies i la web, però d'una manera diferent. Al final triem una sola solució, que és la que es dissenya en la resta de documents i la que es pressuposta en [06-pressupost.md](06-pressupost.md).

## 2.2. Alternativa A: solució al núvol (hosting + Microsoft 365)

**Idea:** l'empresa no compra servidors. Els fitxers i el correu van a Microsoft 365 i la web a un hosting extern.

| Element | Com es resol |
|---|---|
| Fitxers i comptes | Microsoft 365 Empresa Básico (OneDrive/SharePoint, 1 compte per treballador) |
| Web corporativa | Hosting compartit (Raiola Networks, pla Inicio) |
| Xarxa local | Router de l'operador + switch + punt d'accés |
| Còpies | Les fa el proveïdor del núvol |
| DMZ / tallafoc | No cal DMZ pròpia: la web està fora de l'empresa |

**Costos aproximats (IVA inclòs):**

| Concepte | Càlcul | Cost |
|---|---|---|
| Microsoft 365 Empresa Básico | 6,07 €/usuari/mes sense IVA × 3 usuaris × 12 mesos + 21 % | 264,41 €/any |
| Hosting Raiola Inicio | 8,95 €/mes sense IVA × 12 + 21 % | 129,95 €/any |
| Maquinari de xarxa (switch + AP + cables) | Mateixos preus que la solució B | ≈ 281 € (una vegada) |
| Mà d'obra (10 h × 35 €/h) | Configuració de comptes i xarxa | 350 € (una vegada) |
| **Total en 5 anys** | 631 € + 5 × 394,36 € | **≈ 2.603 €** |

**Avantatges:** inversió inicial baixa, no cal mantindre servidors, accés des de fora de l'empresa.

**Limitacions:**
- Si cau Internet no es pot treballar amb els fitxers ni imprimir des de documents del núvol.
- Pagament cada mes per a sempre; el preu pot pujar.
- Els comptes de M365 Básico no fan de domini per als PC (cal un pla més car, Business Premium).
- No resol la xarxa de taller: els equips dels clients estarien en la mateixa xarxa que els PC.
- No permet controlar el portal de seguiment de reparacions (necessitat N8) amb les nostres pròpies dades.

## 2.3. Alternativa B: infraestructura local amb servidors propis i DMZ (TRIADA)

**Idea:** l'empresa té els seus propis servidors i un servidor de comunicacions que separa la xarxa en zones.

| Element | Com es resol |
|---|---|
| Servidor de comunicacions | `tr-router`: Protectli Vault V1410 amb Ubuntu Server (encaminador + tallafoc + NAT + DHCP) |
| Fitxers i comptes | `tr-srv-intern`: Dell PowerEdge T160 amb Windows Server 2025 Essentials (domini, carpetes, impressió) |
| Web + portal QR | `tr-dmz-web`: Mini PC N100 amb Ubuntu Server, Apache, PHP i MariaDB, dins la DMZ |
| Xarxes | LAN, DMZ i xarxa de taller separades (doc. 04) |
| Còpies | Windows Server Backup cada dia + 2 discos en rotació (un sempre fora de l'empresa) |
| Electricitat | SAI APC 1200 VA |

**Costos (detall en [06-pressupost.md](06-pressupost.md)):**

| Concepte | Cost |
|---|---|
| Inversió inicial (maquinari, llicència, domini i mà d'obra) | 6.033,85 € |
| Cost anual (renovació del domini .es) | 8,46 €/any |
| **Total en 5 anys** | 6.033,85 € + 4 × 8,46 € = **6.067,69 €** |

**Avantatges:**
- La xarxa interna funciona encara que caiga Internet (fitxers, impressió, inici de sessió).
- Les dades de clients queden en equips de l'empresa (més control per al RGPD).
- Permet la DMZ i la xarxa de taller, que milloren molt la seguretat.
- No hi ha quotes mensuals: el cost repartit en 5 anys és ≈ 1.214 €/any.
- Els tres treballadors són tècnics informàtics: poden fer el manteniment bàsic.

**Limitacions:**
- Inversió inicial més alta que l'alternativa A.
- Cal fer manteniment (actualitzacions, revisar les còpies).
- El servidor té un sol disc (sense RAID). Ho compensem amb còpies diàries (veure 2.6).

## 2.4. Comparació i decisió del grup

| Criteri | Alternativa A (núvol) | Alternativa B (local + DMZ) |
|---|---|---|
| Cost en 5 anys | ≈ 2.603 € | ≈ 6.068 € |
| Funciona sense Internet | No | Sí (treball intern) |
| Comptes centralitzats en els PC | No (amb el pla Básico) | Sí (domini Windows Server) |
| Separació dels equips dels clients | No | Sí (xarxa de taller) |
| Web separada de la xarxa interna | Sí (hosting extern) | Sí (DMZ pròpia) |
| Portal de reparacions amb dades pròpies | Difícil | Sí |
| Quotes mensuals | Sí | No |
| Coneixements necessaris | Baixos | Mitjans (els tenim: 2n SMX + tècnics de l'empresa) |

**Decisió:** el grup tria l'**alternativa B**. Ho vam decidir els dos membres en la reunió de planificació del Bloc 2 (targeta de Trello «Estudi d'alternatives»), després de comparar la taula anterior.

**Per què:** l'alternativa A és més barata, però no resol tres necessitats importants: comptes centralitzats (N3), xarxa separada per als equips dels clients (N9) i el portal de reparacions (N8). A més, B permet treballar encara que falle Internet. El cost extra (≈ 3.465 € en 5 anys, ≈ 693 €/any) és assumible per a una empresa que factura 60.000 €/any.

**Opció descartada dins de B:** posar tots els servidors com a màquines virtuals en un sol ordinador. És més barat, però si eixe ordinador falla cau tot (també el tallafoc), i la DMZ estaria en el mateix maquinari que la xarxa interna. Per això separem els tres equips físicament.

> **Unificació de la proposta:** en la versió anterior parlàvem d'una solució híbrida amb núvol però pressupostàvem servidors físics. Ara la proposta és **només l'alternativa B**: no s'utilitza cap servei de núvol per a fitxers. Els únics serveis externs són el domini `.es` i la connexió a Internet que ja té l'empresa.

## 2.5. Aspecte innovador: seguiment de reparacions amb codi QR

**Què és:** quan un client deixa un equip, el tècnic crea la reparació en el portal web i imprimeix dues etiquetes amb un **codi QR** (Brother QL-800): una per a l'equip i una per al resguard del client. El client escaneja el QR amb el mòbil i veu l'estat:

`Rebut → En diagnòstic → Esperant peça → Reparat → Llest per a recollir`

**Com funciona tècnicament:**
- El portal és una aplicació PHP + MariaDB en `tr-dmz-web` (DMZ), publicada per HTTPS amb un certificat gratuït de Let's Encrypt.
- Els tècnics canvien l'estat des dels PC de la LAN (el tallafoc deixa LAN → DMZ pel port 443).
- La base de dades de la DMZ només guarda **codi, estat i data**. No guarda nom, telèfon ni DNI del client (eixes dades queden en el servidor intern). Així, si atacaren la web, no hi hauria dades personals (minimització del RGPD).
- L'etiqueta QR en l'equip també serveix d'inventari intern: el tècnic sap de qui és cada equip del taller.

**Utilitat per a l'empresa:**

| Problema actual | Millora amb el QR |
|---|---|
| Els clients telefonen per a preguntar l'estat | Ho consulten sols, a qualsevol hora |
| Es pot confondre un equip amb un altre | Cada equip porta la seua etiqueta única |
| Poca transparència (estratègia del Bloc 1) | El client veu cada pas de la reparació |

**Cost:** etiquetadora QL-800 (74,29 €). El programari és lliure i l'editor d'etiquetes P-touch Editor ve amb la impressora. És una innovació barata, útil i que aprofita la DMZ.

## 2.6. Estudi de viabilitat

### a) Viabilitat dels espais

El local és xicotet. Els servidors van en un racó tècnic al costat del router de l'operador: el T160 és una torre compacta, el Protectli i el mini PC són dispositius xicotets i el switch es pot posar sobre la taula o a la paret. El punt d'accés va al sostre del local, connectat amb un cable de 5 m. No cal obra.

### b) Viabilitat de coneixements

L'equip d'implantació (2n SMX) coneix Ubuntu Server, Windows Server, DHCP, encaminament i NAT (ja ho provem en el Sprint 2 amb màquines virtuals). Els treballadors de TecnoReparo són tècnics informàtics i poden fer el manteniment bàsic després d'una sessió de formació.

### c) Viabilitat tècnica (comprovacions)

**Servidors:**

| Equip | Requisit | Característica del producte | Compleix? |
|---|---|---|---|
| Windows Server 2025 (Desktop Experience) | CPU x64 ≥ 1,4 GHz, RAM ≥ 2 GB (4 GB recomanat), disc ≥ 32 GB, xarxa ≥ 1 Gbps | Dell T160: Xeon 6315P 4 nuclis 2,8 GHz, 16 GB DDR5 ECC, 2 TB, 2 × Gigabit | Sí |
| Llicència Essentials | 1 CPU, màxim 10 nuclis, 25 usuaris i 50 dispositius | 1 CPU de 4 nuclis; 3 usuaris i < 15 dispositius | Sí |
| Llicència ROK de Dell | Només en servidors Dell PowerEdge | El servidor és un Dell PowerEdge | Sí |
| `tr-router` (Ubuntu Server) | 3 interfícies (WAN, LAN, DMZ) + 1 de taller | Protectli V1410: 4 × 2,5 GbE Intel i226-V, 8 GB RAM, 32 GB eMMC | Sí (4 de 4 ports usats) |
| `tr-dmz-web` (Ubuntu Server + Apache) | 1 targeta de xarxa, ≥ 2 GB RAM, ≥ 25 GB disc | Leotec N100: 8 GB RAM, SSD 128 GB, 2 × Gigabit | Sí |

Notes: TPM 2.0 i Secure Boot només són obligatoris per a algunes funcions de Windows Server 2025 (BitLocker, *Secured-core*), no per a instal·lar-lo. El Protectli recomana un disc NVMe per a sistemes grans; per a un encaminador amb Ubuntu Server (≈ 5 GB) els 32 GB d'eMMC són suficients, i es pot afegir un NVMe més endavant.

**Connexions del router i del switch:**

| Dispositiu | Ports necessaris | Ports disponibles |
|---|---|---|
| `tr-router` | WAN (operador), LAN (switch), DMZ (web), TALLER (banc de proves) = 4 | 4 |
| Switch TL-SG1016PE | `tr-router`, servidor, 3 PC, impressora, AP = 7 | 16 (queden 9 lliures) |
| PoE del switch | AP U6+: màxim 9 W, estàndard 802.3af | 8 ports PoE+ (802.3af/at), fins a 30 W per port |

El U6+ es ven **sense injector PoE**: per això triem un switch PoE+ (abans l'AP estava connectat a un PC, cosa que no funcionava). Ara l'AP està connectat directament al switch.

**Compatibilitat dels equips clients:**
- Els 3 PC tenen Windows 11 Pro. L'edició Pro és necessària per a unir-los al domini (Windows 11 Home no pot).
- El portàtil del taller usa Ubuntu Desktop 26.04 (eines de diagnòstic lliures). Accedeix a les carpetes per SMB i no cal que estiga en el domini.
- La impressora multifunció del Bloc 1 té connexió de xarxa: rep una IP fixa (.30).
- L'etiquetadora QL-800 es connecta per USB al PC de reparació (té controladors per a Windows).

**SAI:** consum aproximat del servidor (≈ 100 W), tallafoc (≈ 15 W), mini PC (≈ 15 W) i switch amb AP (≈ 25 W) = ≈ 155 W. El SAI dona 650 W i té 4 endolls: servidor, tallafoc, switch i mini PC web. El router de l'operador va a un endoll normal.

**Separació de xarxes i adreçament:** les xarxes 192.168.1.0/24 (operador), 192.168.10.0/24 (LAN), 192.168.20.0/24 (DMZ) i 192.168.30.0/24 (taller) no se solapen. La comprovació de cada IP està en [04-adrecament-ip.md](04-adrecament-ip.md).

**Publicació de la web:** el router de l'operador envia el trànsit entrant a `tr-router` (mode *bridge* o *DMZ host*). `tr-router` fa DNAT dels ports 80 i 443 cap a 192.168.20.10. Si la IP pública és dinàmica, s'actualitza el registre DNS del domini amb un client de DNS dinàmic.

### d) Viabilitat econòmica

- Inversió total: **6.033,85 €** (IVA inclòs), que és el 10 % de la facturació d'un any.
- Repartit en 5 anys de vida útil: ≈ 1.207 €/any (≈ 2 % de la facturació anual).
- No hi ha quotes mensuals; només 8,46 €/any del domini.
- Conclusió: la inversió és raonable per a TecnoReparo i es pot pagar en un sol any o en terminis.

## 2.7. Fonts consultades

- Microsoft – Requisits de Windows Server: <https://learn.microsoft.com/es-es/windows-server/get-started/system-requirements>
- Microsoft – Preus de Microsoft 365 Empresa Básico: <https://www.microsoft.com/es-es/microsoft-365/sharepoint/sharepoint-business-plans-and-pricing>
- Raiola Networks – Preus de hosting (comparativa WHTop): <https://www.whtop.com/es/compare/arsys.es,raiolanetworks>
- PcComponentes – Llicència Windows Server 2025 Essentials Dell (25 usuaris / 50 dispositius / 10 nuclis): <https://www.pccomponentes.com/licencia-windows-server-2025-essentials-dell-634-cvdt-oem-1-licencia>
- PcComponentes – Dell PowerEdge T160: <https://www.pccomponentes.com/servidor-dell-poweredge-t160-intel-xeon-6315p-16gb-2tb-tower-no-os>
- Protectli – Vault V1410: <https://eu.protectli.com/product/v1410/>
- PcComponentes – Switch TP-Link TL-SG1016PE: <https://www.pccomponentes.com/tp-link-tl-sg1016pe-switch-gestionado-16-puertos-gigabit-8-puertos-poe-plus>
- PcComponentes – Ubiquiti U6+ sense injector PoE: <https://www.pccomponentes.com/ubiquiti-unifi-u6-plus-punto-de-acceso-rj45-sin-inyector-poe>
- PcComponentes – Brother QL-800 (codis QR): <https://www.pccomponentes.com/brother-ql-800-impresora-etiquetas-termica>
- INCIBE – DMZ: <https://www.incibe.es/empresas/blog/dmz-y-te-puede-ayudar-proteger-tu-empresa>
- INCIBE – Còpies de seguretat 3-2-1: <https://www.incibe.es/empresas/blog/copias-seguridad-guia-aproximacion-el-empresario>
- Let's Encrypt (certificats gratuïts): <https://letsencrypt.org/>
