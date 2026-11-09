# 5. Recursos materials i programari

## Introducció

Per a implementar la solució TIC de TecnoReparo serà necessari disposar d'equips informàtics, dispositius de xarxa, sistemes operatius i aplicacions.

Es reutilitzaran els tres ordinadors de sobretaula existents i s'incorporaran dos servidors físics reacondicionats: un per als serveis interns i un altre per a allotjar la web corporativa en una DMZ. Aquesta separació permet organitzar els serveis i millorar la seguretat de la infraestructura.

## Recursos materials

| **Recurs** | **Quantitat** | **Funció** | **Requisits principals** | **Justificació** |
|---|---:|---|---|---|
| Ordinador de sobretaula | 3 | Equip de treball dels tres departaments | Processador actual, 8 GB de RAM com a mínim i connexió Ethernet | Permet realitzar les tasques administratives, tècniques i d'assistència. |
| Servidor físic per a serveis interns | 1 | Centralitzar els serveis interns i els fitxers compartits | Processador multinúcli, 16 GB de RAM, SSD i connexió Gigabit Ethernet | Facilita la gestió dels recursos i la informació de l'empresa. |
| Servidor físic per a la DMZ | 1 | Allotjar i publicar la web corporativa | Processador multinúcli, 8 GB de RAM com a mínim, SSD i connexió Ethernet | Permet separar el servei públic de la xarxa interna. |
| Router/firewall | 1 | Connectar la xarxa amb Internet i controlar el trànsit | Ethernet Gigabit, firewall i suport per a xarxes separades | Protegeix i organitza les comunicacions. |
| Switch Gigabit de 8 ports | 1 | Connectar els equips de la xarxa local | 8 ports Gigabit Ethernet | Proporciona connectivitat cablejada estable i possibilitat d'ampliació. |
| Punt d'accés Wi-Fi | 1 | Connectar dispositius sense fil autoritzats | Wi-Fi 5 o superior i seguretat WPA2/WPA3 | Permet la connexió de dispositius mòbils. |
| Cablejat Ethernet | 1 lot | Connectar els equips i dispositius de xarxa | Cable UTP Cat 6 | Assegura una connexió cablejada adequada. |
| Disc dur extern per a còpies | 1 | Realitzar còpies de seguretat | Capacitat suficient i connexió USB 3.0 | Permet conservar una còpia local de la informació important. |

## Recursos de programari

| **Programari** | **Quantitat** | **Funció** | **Justificació** |
|---|---:|---|---|
| Sistema operatiu Linux per als servidors | 2 | Gestionar els servidors interns i el servidor web de la DMZ | És un sistema estable, flexible i de cost de llicència nul. |
| Sistema operatiu d'escriptori | 3 | Gestionar els ordinadors clients | Permet executar les aplicacions necessàries per als treballadors. Es reutilitzaran els sistemes instal·lats, si són compatibles. |
| Suite ofimàtica lliure | 3 | Crear i editar documents, fulls de càlcul i presentacions | Permet realitzar les tasques administratives sense costos de llicència. |
| Navegador web | 3 | Accedir a la web corporativa i als serveis d'Internet | És necessari per a la navegació i l'accés als serveis web. |
| Servidor web Apache | 1 | Publicar la web corporativa | Permet allotjar la web en el servidor situat en la DMZ. |
| Programari de còpies de seguretat | 1 | Realitzar i gestionar còpies de seguretat | Ajuda a protegir la informació davant possibles pèrdues. |
| Firewall del router | 1 | Filtrar i controlar el trànsit de xarxa | Permet aplicar mesures de seguretat i controlar les comunicacions entre xarxes. |

## Justificació dels recursos

Els recursos seleccionats permeten implementar la infraestructura local amb dos servidors físics independents. El servidor intern centralitzarà els serveis de l'empresa, mentre que el servidor web es trobarà en una DMZ per a reduir l'exposició de la xarxa interna.

La reutilització dels ordinadors clients i l'ús de servidors reacondicionats permeten reduir la inversió inicial. A més, l'ús de sistemes operatius i aplicacions lliures o gratuïtes contribueix a mantindre els costos de programari baixos.

La relació detallada dels costos es presenta en `06-pressupost.md`.
