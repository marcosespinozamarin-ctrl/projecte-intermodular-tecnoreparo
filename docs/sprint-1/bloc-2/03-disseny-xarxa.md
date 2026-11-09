# 3. Disseny de la xarxa

## 3.1. Introducció

En aquest apartat es presenta el disseny de la xarxa informàtica proposada per a l'empresa TecnoReparo.

La xarxa està dissenyada per a connectar els equips de treball i els servidors, permetent la comunicació entre els dispositius i l'accés als serveis de l'empresa.

## 3.2. Esquema de la xarxa

A continuació es mostra l'esquema de la xarxa proposada per a TecnoReparo.

![Disseny de la xarxa de TecnoReparo](<img/Captura de pantalla de 2026-11-09 10-27-40.png>)

## 3.3. Descripció de la infraestructura

La infraestructura de xarxa està formada pels elements següents:

- **Router/firewall:** permet la connexió amb Internet i protegeix la xarxa interna.
- **Switch:** connecta els dispositius de la xarxa local mitjançant cable Ethernet.
- **Punt d'accés Wi-Fi:** proporciona connectivitat sense fils.
- **Equips de treball:** ordinadors utilitzats pels treballadors de TecnoReparo.
- **Servidor intern:** centralitza els serveis i recursos interns de l'empresa.
- **Servidor web en DMZ:** allotja el servei web en una zona separada de la xarxa interna.
- **Cablejat Ethernet Cat 6:** permet la connexió cablejada dels dispositius.

## 3.4. Organització de la xarxa

La xarxa es divideix en una xarxa interna i una zona DMZ.

La xarxa interna conté els equips de treball i el servidor intern. La DMZ està destinada al servidor web, de manera que els serveis accessibles des de l'exterior queden separats de la xarxa interna.

El router/firewall controla el trànsit entre Internet, la xarxa interna i la DMZ.

## 3.5. Justificació del disseny

Aquest disseny permet organitzar els dispositius de manera clara i millorar la seguretat de la infraestructura TIC.

La separació del servidor web en una DMZ redueix l'exposició de la xarxa interna. A més, l'ús d'un switch i de cablejat Ethernet facilita una connexió estable entre els equips.
