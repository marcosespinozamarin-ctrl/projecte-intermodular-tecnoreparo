# 2. Màquines virtuals

En aquest apartat creem les cinc màquines virtuals de TecnoReparo i instal·lem els sistemes operatius.

## 2.1. Taula de màquines virtuals

| Màquina | Funció | Sistema i versió | RAM | CPU | Disc | Amfitrió |
|---|---|---|---|---|---|---|
| `tr-router` | Servidor de comunicacions | Ubuntu Server 24.04 LTS | 1 GB | 1 | 20 GB | PC de Marcos |
| `tr-srv-intern` | Servidor intern | Windows Server 2025 | 3 GB | 2 | 50 GB | PC de Marcos |
| `tr-client-win` | Client Windows | Windows 11 | 4 GB | 2 | 64 GB | PC de Marcos |
| `tr-client-lin` | Client Linux | Ubuntu Desktop 24.04 LTS | 2 GB | 2 | 25 GB | PC de Marcos |
| `tr-dmz-web` | Servidor de la DMZ | Ubuntu Server 24.04 LTS | 1 GB | 1 | 20 GB | PC de Marcos |

## 2.2. Decisions d'instal·lació

- **Servidors Linux sense entorn gràfic:** `tr-router` i `tr-dmz-web` usen Ubuntu Server perquè només necessiten la terminal. Així gasten menys RAM i disc.
- **Windows Server amb entorn d'escriptori:** instal·lem l'opció *Desktop Experience* per a gestionar-lo més fàcilment. Encara no instal·lem Active Directory; ho farem en el Sprint 3.
- **Windows 11:** li donem 4 GB de RAM i 64 GB de disc perquè són els mínims que demana el sistema. Activem EFI i TPM en VirtualBox.
- **Discos dinàmics:** tots els discos virtuals són de mida dinàmica perquè només ocupen l'espai que usen.
- **Noms dels equips:** cada sistema té el mateix nom que la seua màquina virtual.
- **Instantànies:** fem una instantània de cada màquina després d'instal·lar-la, abans de configurar la xarxa.

## 2.3. Comprovació de les MAC

Si cloneu alguna màquina, VirtualBox ha de generar una MAC nova. Comprovem que totes les adreces MAC són diferents:

| Màquina | Adaptador | MAC |
|---|---|---|
| `tr-router` | Adaptador 1 (NAT) | *(per omplir)* |
| `tr-router` | Adaptador 2 (`tr-lan`) | *(per omplir)* |
| `tr-router` | Adaptador 3 (`tr-dmz`) | *(per omplir)* |
| `tr-srv-intern` | Adaptador 1 (`tr-lan`) | *(per omplir)* |
| `tr-client-win` | Adaptador 1 (`tr-lan`) | *(per omplir)* |
| `tr-client-lin` | Adaptador 1 (`tr-lan`) | *(per omplir)* |
| `tr-dmz-web` | Adaptador 1 (`tr-dmz`) | *(per omplir)* |

## 2.4. Captures

### `tr-router`
![Sessió iniciada en tr-router](../../img/sprint-2/02-tr-router.png)
*Ubuntu Server instal·lat i sessió iniciada en `tr-router`.*

### `tr-srv-intern`
![Sessió iniciada en tr-srv-intern](../../img/sprint-2/02-tr-srv-intern.png)
*Windows Server 2025 instal·lat i sessió iniciada en `tr-srv-intern`.*

### `tr-client-win`
![Sessió iniciada en tr-client-win](../../img/sprint-2/02-tr-client-win.png)
*Windows 11 instal·lat i sessió iniciada en `tr-client-win`.*

### `tr-client-lin`
![Sessió iniciada en tr-client-lin](../../img/sprint-2/02-tr-client-lin.png)
*Ubuntu Desktop instal·lat i sessió iniciada en `tr-client-lin`.*

### `tr-dmz-web`
![Sessió iniciada en tr-dmz-web](../../img/sprint-2/02-tr-dmz-web.png)
*Ubuntu Server instal·lat i sessió iniciada en `tr-dmz-web`.*

### Llista de màquines en VirtualBox
![Màquines en VirtualBox](../../img/sprint-2/02-virtualbox.png)
*Les cinc màquines creades en VirtualBox.*
