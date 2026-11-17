# 1. Identificació de les necessitats TIC

## 1.1. Introducció

TecnoReparo és una microempresa de Banyeres de Mariola que repara i manté equips informàtics. Té **3 treballadors** repartits en tres departaments (Bloc 1): direcció i administració, reparació i manteniment, i assistència tècnica.

Per a detectar les necessitats hem revisat les funcions de cada treballador, els equips que ja té l'empresa i la forma de treballar d'un taller de reparació (els equips dels clients entren, es reparen i es tornen).

## 1.2. Situació actual (punt de partida)

| Element | Situació actual (Bloc 1) | Problema detectat |
|---|---|---|
| Ordinadors | 3 PC de sobretaula + 1 portàtil | No hi ha comptes centralitzats: cada PC té usuaris locals |
| Documents | Guardats en cada PC, en un servei d'emmagatzematge al núvol i en un disc extern | No hi ha permisos per departament ni comptes centralitzats, i sense Internet no es pot accedir als documents del núvol. La nova solució (alternativa B) passa els documents al servidor intern i deixa d'usar el núvol. |
| Xarxa | Router de l'operador | Tots els equips estan en la mateixa xarxa, també els equips dels clients |
| Web | No en té | Els clients no poden consultar serveis ni l'estat de la reparació |
| Còpies | 1 disc extern | No hi ha còpia fora de l'empresa ni planificació |

## 1.3. Taula de necessitats

| Núm. | Departament | Necessitat TIC | Usuaris afectats | Justificació |
|---|---|---|---|---|
| N1 | Tots | Xarxa interna cablejada i Wi-Fi segura | 3 treballadors + portàtil | Els PC, el servidor i la impressora s'han de comunicar. El portàtil del taller necessita Wi-Fi per a moure's pel local. |
| N2 | Tots | Accés a Internet | 3 treballadors | Correu, proveïdors, controladors, manuals i actualitzacions. |
| N3 | Tots | Comptes d'usuari centralitzats i permisos | 3 treballadors | Cada persona entra amb el seu usuari i només veu les carpetes del seu departament (control d'accés i RGPD). |
| N4 | Tots | Compartició de fitxers | 3 treballadors | Una carpeta comuna i una per departament, guardades en el servidor i no en cada PC. |
| N5 | Direcció i administració | Impressió i escaneig en xarxa | 3 treballadors (sobretot direcció) | Pressupostos, factures i resguards de reparació. |
| N6 | Direcció i administració | Còpies de seguretat automàtiques | 3 treballadors | Factures i dades de clients no es poden perdre. Cal seguir la regla 3-2-1 que recomana INCIBE. |
| N7 | Empresa / clients | Web corporativa | Clients + direcció | Donar a conéixer els serveis, horaris i contacte. |
| N8 | Reparació i assistència | Seguiment de reparacions per al client | 2 tècnics + clients | Ara els clients telefonen per saber com va la reparació. Una consulta web amb codi QR estalvia temps (veure innovació, doc. 02). |
| N9 | Reparació i manteniment | Xarxa separada per als equips dels clients | 1 tècnic (taller) | Els equips que arriben poden tindre virus. Si es connecten a la xarxa interna poden infectar el servidor. Necessiten Internet per a actualitzar, però aïllats. |
| N10 | Tots | Seguretat perimetral (tallafoc) i DMZ | Tota l'empresa | La web és pública: ha d'estar separada de la xarxa interna perquè un atac a la web no arribe als PC ni al servidor. |
| N11 | Tots | Alimentació protegida (SAI) | Tota l'empresa | Un tall de llum pot fer malbé el servidor o les dades. |

## 1.4. Relació necessitat → solució

| Necessitat | Element de la solució (detallat en els documents 03, 04 i 05) |
|---|---|
| N1, N2 | Switch Gigabit PoE, punt d'accés Wi-Fi U6+ i servidor de comunicacions `tr-router` |
| N3, N4 | Servidor intern `tr-srv-intern` amb Windows Server 2025 Essentials (domini i carpetes compartides) |
| N5 | Impressora multifunció amb IP fixa |
| N6 | Windows Server Backup + 2 discos externs en rotació |
| N7, N8 | Servidor web `tr-dmz-web` en la DMZ + etiquetadora de codis QR |
| N9 | Xarxa de taller 192.168.30.0/24 (només Internet) |
| N10 | `tr-router` amb tallafoc i 3 xarxes separades |
| N11 | SAI APC BX1200MI-GR |

## 1.5. Fonts consultades

- Documents del Bloc 1: [empresa](../01-empresa.md), [organització](../02-organitzacio.md), [recursos TIC](../03-recursos-tic.md) i [maquinari i programari](../04-maquinari-programari.md).
- Enunciat de l'activitat PI-Q.1.2.
- INCIBE – *Copias de seguridad: una guía de aproximación para el empresario* (regla 3-2-1): <https://www.incibe.es/empresas/blog/copias-seguridad-guia-aproximacion-el-empresario>
- INCIBE – *Qué es una DMZ y cómo te puede ayudar a proteger tu empresa*: <https://www.incibe.es/empresas/blog/dmz-y-te-puede-ayudar-proteger-tu-empresa>
- INCIBE – *Protege tu escaparate en Internet* (web pròpia o hosting): <https://www.incibe.es/empresas/blog/protege-tu-escaparate-internet>
