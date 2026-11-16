# 1. Pla d'intervenció

## 1.1. Introducció

En aquest sprint posarem en marxa la infraestructura de TecnoReparo que vam dissenyar en el Sprint 1. Crearem les màquines virtuals, instal·larem els sistemes operatius i configurarem la xarxa interna (LAN), la DMZ, l'encaminament i el servei DHCP.

Abans de començar, hem preparat aquest pla per a saber quines tasques farem, en quin ordre, qui les farà i quins recursos necessitem.

## 1.2. Canvis respecte al Sprint 1

Mantenim l'adreçament de la SA1: la LAN utilitza `192.168.10.0/24` i la DMZ `192.168.20.0/24`.

L'únic canvi és el nom d'un equip. En el Sprint 1 vam anomenar "servidor de comunicacions" al servidor intern (`192.168.10.20`). En aquest sprint, el servidor de comunicacions és el servidor Linux que fa de router entre les xarxes. Per això, el servidor amb l'adreça `192.168.10.20` ara s'anomena **servidor intern**.

| Equip | Nom | Adreça IP |
|---|---|---|
| Servidor de comunicacions (router) | `tr-router` | LAN `192.168.10.1` · DMZ `192.168.20.1` · exterior per NAT |
| Servidor intern | `tr-srv-intern` | `192.168.10.20` |
| Servidor de la DMZ | `tr-dmz-web` | `192.168.20.10` |
| Client Windows | `tr-client-win` | DHCP |
| Client Linux | `tr-client-lin` | DHCP |

## 1.3. Seqüència de tasques i temps previst

L'activitat dura 5 setmanes (10 hores), és a dir, unes 2 hores per setmana.

| Núm. | Tasca | Depén de | Setmana | Temps previst | Responsable | Col·laborador |
|---|---|---|---|---|---|---|
| 1 | Pla d'intervenció i tauler de Trello | — | 1 | 1 h | Marcos | Nicolas |
| 2 | Creació de les màquines virtuals i instal·lació dels sistemes | 1 | 1–2 | 2,5 h | Nicolas | Marcos |
| 3 | Configuració de la LAN, la DMZ i l'adreçament + diagrama | 2 | 2–3 | 1,5 h | Marcos | Nicolas |
| 4 | Configuració del servidor de comunicacions i de l'encaminament | 3 | 3 | 1,5 h | Marcos | Nicolas |
| 5 | Instal·lació i configuració del servei DHCP | 4 | 4 | 1,5 h | Nicolas | Marcos |
| 6 | Proves de connectivitat i validació | 5 | 4–5 | 1,5 h | Nicolas | Marcos |
| 7 | Seguiment, incidències i revisió final | — | 1–5 | 0,5 h | Marcos i Nicolas | — |
| | **Total** | | | **10 h** | | |

Les tasques s'han de fer en ordre, perquè cada una necessita l'anterior: sense màquines no podem configurar la xarxa, sense xarxa no hi ha encaminament, i sense encaminament i DHCP no podem fer les proves. La tasca 7 es fa durant tot el sprint, al final de cada sessió.

## 1.4. Recursos necessaris

### Ordinador amfitrió

Totes les màquines virtuals estaran en un sol ordinador, el de Marcos.

| Recurs | Valor |
|---|---|
| Memòria RAM | 16 GB |
| Espai lliure en disc | 200 GB |
| Processador | 8 nuclis amb virtualització activada (AMD-V / VT-x) |
| Hipervisor | VirtualBox |

### Màquines virtuals

| Màquina | Funció | Sistema | RAM | CPU | Disc |
|---|---|---|---|---|---|
| `tr-router` | Servidor de comunicacions | Ubuntu Server 24.04 LTS | 1 GB | 1 | 20 GB |
| `tr-srv-intern` | Servidor intern | Windows Server 2025 | 3 GB | 2 | 50 GB |
| `tr-client-win` | Client Windows | Windows 11 | 4 GB | 2 | 64 GB |
| `tr-client-lin` | Client Linux | Ubuntu Desktop 24.04 LTS | 2 GB | 2 | 25 GB |
| `tr-dmz-web` | Servidor de la DMZ | Ubuntu Server 24.04 LTS | 1 GB | 1 | 20 GB |
| **Total** | | | **11 GB** | | **179 GB** |

Amb 16 GB de RAM podem tindre les cinc màquines enceses alhora i encara queda memòria per a l'ordinador amfitrió.

### Imatges i programari

- Imatges ISO: Ubuntu Server 24.04 LTS, Ubuntu Desktop 24.04 LTS, Windows Server 2025 i Windows 11.
- VirtualBox.
- GitHub i Markdown per a la documentació.
- Trello per a organitzar les tasques.
- Un editor de diagrames per a actualitzar l'esquema de la xarxa.

## 1.5. Distribució de les màquines i xarxes virtuals

Com que les cinc màquines estan en el mateix ordinador, totes poden comunicar-se a través de les xarxes internes de VirtualBox. Si les màquines estigueren en dos ordinadors diferents, no es connectarien encara que les xarxes internes tingueren el mateix nom.

| Xarxa | Tipus en VirtualBox | Nom | Equips connectats |
|---|---|---|---|
| Exterior | NAT | — | `tr-router` |
| LAN | Xarxa interna | `tr-lan` | `tr-router`, `tr-srv-intern`, `tr-client-win`, `tr-client-lin` |
| DMZ | Xarxa interna | `tr-dmz` | `tr-router`, `tr-dmz-web` |

El servidor de comunicacions té tres adaptadors (exterior, LAN i DMZ). La resta d'equips només tenen l'adaptador de la seua xarxa, perquè tot el trànsit passe pel servidor de comunicacions.

## 1.6. Permisos i autoritzacions

- **Instal·lació de programari:** cal permís del professorat per a instal·lar VirtualBox o crear màquines virtuals en els ordinadors de l'aula.
- **Llicències de Windows:** utilitzarem versions d'avaluació de Windows Server 2025 i Windows 11, o les llicències que ens indique el centre.
- **Canvis en la xarxa:** les xarxes internes de VirtualBox no afecten la xarxa de l'aula. No canviarem la configuració de xarxa de l'ordinador amfitrió sense permís del professorat.
- **Repositori i Trello:** el professorat ha de tindre accés al repositori privat de GitHub i al tauler de Trello.

## 1.7. Riscos i mesures preventives

| Activitat | Risc | Mesura preventiva | Norma de l'aula relacionada |
|---|---|---|---|
| Treball llarg davant de la pantalla | Cansament visual i mals d'esquena | Fer pauses curtes cada hora, mantindre una bona postura i ajustar la brillantor de la pantalla | Mantindre una postura correcta en el lloc de treball |
| Ús de connexions elèctriques | Descàrregues o curtcircuits | No manipular endolls ni cables amb l'equip encés i avisar el professorat si hi ha algun dany | No manipular les instal·lacions elèctriques de l'aula |
| Instal·lació i configuració dels sistemes | Pèrdua de dades o d'una màquina virtual | Fer instantànies (snapshots) abans de cada canvi important i guardar la documentació en GitHub | Guardar el treball i fer còpies de seguretat |
| Canvis de xarxa | Afectar la xarxa de l'aula o altres equips | Utilitzar només xarxes internes de VirtualBox i no activar DHCP fora de la LAN virtual | No modificar la configuració de xarxa dels equips de l'aula |

**Mitjans de protecció i recuperació:** instantànies de VirtualBox, còpia de la documentació en GitHub i, si cal, un disc extern per a guardar les màquines virtuals.

## 1.8. Imprevistos possibles i solucions

| Imprevist | Solució prevista |
|---|---|
| No hi ha prou memòria RAM per a tindre les cinc màquines enceses | Baixar la RAM de les màquines que ho permeten (per exemple, el client Linux a 1,5 GB) o encendre només les màquines necessàries per a cada prova |
| No hi ha prou espai en disc | Utilitzar discos virtuals de mida dinàmica, esborrar instantànies antigues o moure màquines a un disc extern |
| Una instal·lació no arranca | Revisar que la virtualització està activada en la BIOS, comprovar la imatge ISO i la configuració de la màquina (tipus de sistema, EFI) i, si cal, tornar a crear-la |
| Una màquina deixa de funcionar després d'un canvi | Tornar a l'última instantània guardada |

## 1.9. Organització en Trello i seguiment

Organitzarem les tasques en un tauler de Trello amb tres llistes:

- **Pendent:** tasques que encara no hem començat.
- **En procés:** tasques que estem fent.
- **Finalitzat:** tasques acabades i comprovades.

Cada targeta tindrà el nom de la tasca, una breu descripció i la persona responsable.

**Revisió de cada sessió:** al final de cada sessió, revisarem el tauler, mourem les targetes segons el seu estat i anotarem en el document de seguiment (`07-seguiment-incidencies.md`) què hem fet, el temps utilitzat, els problemes i el treball pendent.

**Comunicació de desviacions:** si un problema endarrereix una tasca i pot afectar el lliurament, ho comunicarem al professorat a classe o per Aules, i anotarem la comunicació i l'acord en el document de seguiment.

Enllaç al tauler de Trello: *(pendent d'afegir)*
