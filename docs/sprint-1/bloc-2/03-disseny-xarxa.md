# 3. Disseny de la xarxa

## Introducció

La xarxa de TecnoReparo permetrà connectar els ordinadors dels tres departaments, compartir recursos i accedir a Internet. Es proposa una topologia en estrella, amb un switch central que connectarà els equips de l'empresa.

La infraestructura inclourà una xarxa interna i una zona desmilitaritzada (DMZ), destinada a allotjar serveis accessibles des de l'exterior de manera controlada.

## Topologia de xarxa

La xarxa estarà formada pels següents elements:

- **Router/Firewall:** connecta la xarxa de l'empresa amb Internet i controla el trànsit entre les xarxes.
- **Switch central:** connecta els ordinadors, el servidor i els dispositius de xarxa.
- **Ordinadors clients:** equips utilitzats pels treballadors dels tres departaments.
- **Servidor de comunicacions:** proporciona serveis interns, com ara gestió d'usuaris, compartició de fitxers i serveis de xarxa.
- **Punt d'accés Wi-Fi:** proporciona connexió sense fil als dispositius autoritzats.
- **DMZ:** xarxa separada on es podrà allotjar el servidor web corporatiu.

## Esquema de la xarxa

L'esquema es representa de manera simplificada:
![Disseny de la xarxa de TecnoReparo](img/Captura%20de%20pantalla%20de%202026-11-09%2010-27-40.png)
```

## Explicació dels components i connexions

El router/firewall serà el punt d'entrada i eixida de la xarxa. Aplicarà les regles de seguretat i permetrà separar la xarxa interna de la DMZ.

El switch central connectarà els ordinadors dels treballadors i el servidor de comunicacions. La connexió cablejada oferirà estabilitat i velocitat als equips de treball.

El punt d'accés Wi-Fi permetrà connectar dispositius sense fil. La xarxa Wi-Fi haurà d'estar protegida amb una contrasenya segura i, si és possible, separada de la xarxa interna.

El servidor de comunicacions oferirà serveis interns com la gestió d'usuaris, l'emmagatzematge compartit i les còpies de seguretat.

## Serveis de la DMZ

La DMZ allotjarà el servidor web corporatiu de TecnoReparo. Aquest servidor permetrà publicar informació de l'empresa, com ara els serveis de reparació, les dades de contacte i els horaris.

El servidor web estarà separat de la xarxa interna per a reduir el risc que un accés extern no autoritzat afecte els equips i les dades dels treballadors.

## Fonts consultades

- Apunts de classe sobre topologies de xarxa, dispositius de comunicació i DMZ.
- Documentació del Bloc 1 del projecte: organització i recursos TIC.
