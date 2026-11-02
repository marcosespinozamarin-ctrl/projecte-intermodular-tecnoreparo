
# 4. Adreçament IP

## Introducció

La xarxa de TecnoReparo utilitzarà adreces IP privades per a comunicar els equips dins de la xarxa local. Es dividirà en dues subxarxes: una per a la xarxa interna i una altra per a la DMZ.

Aquesta separació permetrà organitzar els dispositius i aplicar mesures de seguretat diferents segons la funció de cada xarxa.

## Pla d'adreçament

| Equip o grup | Xarxa | Adreça IP prevista | Màscara / prefix | Porta d'enllaç |
|---|---|---|---|---|
| Router - xarxa interna | Interna | 192.168.10.1 | 255.255.255.0 /24 | — |
| Ordinadors clients | Interna | 192.168.10.10 - 192.168.10.12 | 255.255.255.0 /24 | 192.168.10.1 |
| Servidor de comunicacions | Interna | 192.168.10.20 | 255.255.255.0 /24 | 192.168.10.1 |
| Punt d'accés Wi-Fi | Interna | 192.168.10.30 | 255.255.255.0 /24 | 192.168.10.1 |
| Router - DMZ | DMZ | 192.168.20.1 | 255.255.255.0 /24 | — |
| Servidor web | DMZ | 192.168.20.10 | 255.255.255.0 /24 | 192.168.20.1 |

## Xarxa interna

La xarxa interna utilitzarà el rang `192.168.10.0/24`.

- Adreça de xarxa: `192.168.10.0`
- Porta d'enllaç: `192.168.10.1`
- Rang d'adreces disponibles per a equips: `192.168.10.2 - 192.168.10.254`
- Màscara: `255.255.255.0`

Els ordinadors, el servidor de comunicacions i el punt d'accés Wi-Fi utilitzaran adreces dins d'aquesta subxarxa.

## DMZ

La DMZ utilitzarà el rang `192.168.20.0/24`.

- Adreça de xarxa: `192.168.20.0`
- Porta d'enllaç: `192.168.20.1`
- Rang d'adreces disponibles: `192.168.20.2 - 192.168.20.254`
- Màscara: `255.255.255.0`

El servidor web corporatiu tindrà l'adreça `192.168.20.10`.

## Justificació de la separació

La xarxa interna i la DMZ utilitzen rangs diferents, de manera que no se solapen.

La separació permetrà aplicar regles de firewall per a controlar les comunicacions entre les dues xarxes. El servidor web de la DMZ no tindrà accés lliure als equips interns.

Les adreces IP dels servidors i dispositius de xarxa seran fixes per a facilitar la seua administració. Els ordinadors clients podran configurar-se mitjançant DHCP.
