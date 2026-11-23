# 1. Pla d'intervenció

En aquest sprint implantarem la infraestructura dissenyada en el Sprint 1: màquines virtuals, LAN, DMZ, encaminament i DHCP.

## 1.1. Canvis respecte al Sprint 1

Mantenim l'adreçament: LAN `192.168.10.0/24` i DMZ `192.168.20.0/24`. Només canvia un nom: el servidor `192.168.10.20` ara és el **servidor intern**, i el **servidor de comunicacions** és el router Linux.

## 1.2. Tasques i temps previst

| Núm. | Tasca | Depén de | Setmana | Temps | Responsable | Col·laborador |
|---|---|---|---|---|---|---|
| 1 | Pla d'intervenció i Trello | — | 1 | 1 h | Marcos | Nicolas |
| 2 | Màquines virtuals i sistemes | 1 | 1–2 | 2,5 h | Nicolas | Marcos |
| 3 | Xarxa, adreçament i diagrama | 2 | 2–3 | 1,5 h | Marcos | Nicolas |
| 4 | Servidor de comunicacions | 3 | 3 | 1,5 h | Marcos | Nicolas |
| 5 | Servei DHCP | 4 | 4 | 1,5 h | Nicolas | Marcos |
| 6 | Proves de connectivitat | 5 | 4–5 | 1,5 h | Nicolas | Marcos |
| 7 | Seguiment i revisió final | — | 1–5 | 0,5 h | Tots dos | — |

## 1.3. Recursos

**Ordinador amfitrió (Marcos):** 16 GB de RAM, 200 GB lliures, 8 nuclis amb virtualització activada i VirtualBox.

| Màquina | Sistema | RAM | CPU | Disc | Xarxa |
|---|---|---|---|---|---|
| tr-router | Ubuntu Server 26.04 | 1 GB | 1 | 20 GB | NAT + tr-lan + tr-dmz |
| tr-srv-intern | Windows Server 2025 | 3 GB | 2 | 50 GB | tr-lan |
| tr-client-win | Windows 11 | 4 GB | 2 | 64 GB | tr-lan |
| tr-client-lin | Ubuntu Desktop 26.04 | 2 GB | 2 | 25 GB | tr-lan |
| tr-dmz-web | Ubuntu Server 26.04 | 1 GB | 1 | 20 GB | tr-dmz |

Totes les màquines estan en el mateix ordinador, per això les xarxes internes de VirtualBox es connecten sense problemes. També necessitem les ISO dels sistemes, GitHub, Trello i un editor de diagrames.

## 1.4. Permisos

- Permís del professorat per a utilitzar VirtualBox en l'aula.
- Versions d'avaluació de Windows o llicències del centre.
- No canviarem la xarxa de l'aula: només usarem xarxes internes de VirtualBox.

## 1.5. Riscos i mesures

| Risc | Mesura |
|---|---|
| Cansament per treballar molt de temps davant la pantalla | Pauses curtes i bona postura |
| Accidents amb connexions elèctriques | No tocar cables amb l'equip encés |
| Pèrdua de dades | Instantànies abans de cada canvi i documentació en GitHub |
| Afectar la xarxa de l'aula | Usar només xarxes internes i DHCP només en la LAN virtual |

## 1.6. Imprevistos

| Imprevist | Solució |
|---|---|
| Falta de RAM | Baixar la RAM d'alguna màquina o encendre només les necessàries |
| Falta d'espai en disc | Discos dinàmics i esborrar instantànies antigues |
| Una instal·lació no arranca | Revisar la virtualització en la BIOS i la ISO, o tornar a crear la màquina |

## 1.7. Seguiment

Usarem Trello amb les llistes **Pendent**, **En procés** i **Finalitzat**. Cada targeta tindrà responsable i descripció. Al final de cada sessió actualitzarem Trello i el document de seguiment. Si hi ha un retard que afecte el lliurament, avisarem el professorat.

Tauler de Trello: *(pendent d'afegir)*
