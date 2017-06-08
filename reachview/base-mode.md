## Sortie du flux de correction (Correction output)

<p style="text-align:center"><img src="../img/reachview/base_mode/output.png" style="width: 800px;"/></p>

Le module reach exporte le flux de correction selon le format standard RTCM3. Les données de correction peuvent être transmises par liaison série (Serial), TCP, NTRIP ou LoRa pour Reach RS.

### Liaison Série (Serial)
La connexion au port série est disponible avec différentes options de connexion matérielle. Toutes supportent les vitesses de transmission suivantes: 4800, 9600, 14400, 19200, 28800, 38400, 56000, 57600, 115200, 128000, 153600, 230400, 256000, 460800, 921600

#### UART
Correpond à l'UART TTL du module Reach ou le port RS232 du connecteur d'extension disponible sur le Reach RS. C'est un cas usuel que d'y connecter la radio pour transmettre les données de correction.

#### USB-to-PC
Quand le module Reach est connecté à un ordinateur via USB il sera visible en tant que différents appareils, l'un d'entre eux est via un port série. Vous pouvez utiliser ce port série pour envoyer les données de correction à l'ordinateur.

#### USB OTG
Utiliser un cable micro-USB OTG pour connecter des accessoires USB. Dans ce mode là seulement les appareils USB qui émulent un port série peuvent être utilisés. Exemples de puces répandues qui sont supportées : FT232, CP2102. Il y a de nombreux appareils basés sur ces puces qui peuvent vous fournir un UART TTL ou un port RS232.

### NTRIP
NTRIP est la norme du secteur pour transférer les corrections GNSS via Internet, avec ReachView vous pouvez utiliser tout service publique ou votre propre fournisseur privé. NTRIP ne permet pas une communication point à point, par exemple vous ne pouvez pas l'utiliser pour transmettre les corrections d'un module Reach à un autre directement. Dans la terminolgie NTRIP il y a des serveurs, des clients et des diffuseurs. Le serveur envoie les corrections au diffuseur et les clients peuvent les recevoir en se connectant à ce diffuseur.

Pour envoyer des correction à un diffuseur NTRIP vous avez besoin de:

- l'adresse IP ou nom de domaine du diffuseur
- port
- nom d'utilisateur
- mot de passe
- point de montage

Quand un module Reach est connecté via NTRIP en mode station fixe (base), il agit en tant que serveur NTRIP.

### TCP
Le scénario typique pour utiliser TCP est d'envoyer les données de correction vers une application sur le même réseau ou sur un serveur avec une adresse IP publique.

Le mode TCP supporte deux rôles:

#### Serveur
Vous devez renseigner le port et ensuite les clients seront en mesure de se connecter à cet appareil sur son adresse IP. Plusieurs clients peuvent se connecter au même serveur.
#### Client
Vous devez renseigner l'adresse IP et le numéro du port du serveur.

Si ReachView ne permet pas de renseigner un port spécifique, cela signigie qu'il est utilisé pour un usage internet.

### Radio LoRa (seulement Reach RS)
Le Reach RS possède un radio LoRa interne qui est utilisée pour recevoir et envoyer les corrections. La radio fonctionne dans un seul sens, elle peut être configurée soit pour envoyer des corrections (depuis la station fixe ou base) ou pour les recevoir (récepteur mobile ou rover). En utilisant la modulation LoRa il est possible d'atteindre une portée de 19km en ligne de visée directe ou de quelques kilomètres en zone urbaine avec seulement 20 dBm de puissance de sortie. Tant que les paramètres de fréquence et de vitesse de transmission correspondent il est possible de connecter un nombre infini de récepteur mobile qui peuvent alors recevoir les corrections depuis une seule station fixe (base).

Plus la vitesse de transmission est faible, plus la portée effective sera grande. Selon votre selection de messages RTCM3 ReachView restreindra automatiquement les vitesses de transmission trop faibles. Il faut désactiver des messages de correction ou réduire leur fréquence d'envoi afin de débloquer des vitesses de transmission plus faibles.
Les vitesses de transmission sur les Reach RS émetteurs (base) et récepteurs (rover) doivent correspondre.

Veuillez vérifier que vous sélectionner des puissance d'émission et de fréquence en accord avec la règlementation de votre région.

## Messages RTCM3

<p style="text-align:center"><img src="../img/reachview/base_mode/messages.png" style="width: 800px;"/></p>



|  Messages RTCM3  |  Messages minimaux requis  |    @    |
|------|-----------------------------|---------|
| 1002 |    GPS L1 observations      |  1 Hz   |
| 1006 |    ARP station coordinate   | 0.1 Hz  |



|   Messages RTCM3   | Messages optionnels pour autres systèmes GNSS |
|------|------------------------------------------|
| 1010 |         GLONASS L1 observation           |
| 1097 |			  GALILEO MSM				  |
| 1107 |              SBAS MSM                    |
| 1117 |              QZSS MSM                    |
| 1127 |              BeiDou MSM                  |



|  RTCM3 messages    | Messages spécifiques pour applications atypiques |
|------|------------------------------------------------|
| 1008 |                  Antenna type                  |
| 1019 |              GPS Ephemeris                     |
| 1020 |              GLONASS Ephemeris                 |


Le sous-ensembel minimal nécessaire au fonctionnement en RTK est 1002 pour les observations GPS et 1006 pour les coordonnées de la station fixe (base). Activer plus de messages ou une fréquence d'envoi plus importante requiert une bande passante plus importante pour votre connexion.

Voici une estimation en bps (bit par secondes) quand les messages sont configurés à 1 Hz:
Here is an estimation of bps when messages are configured at 1 Hz:

|   Messages RTCM3   | Vitesse de transmission, bps |
|--------------------|----------------|
| 1002 		         |      156       |
| 1006	  			 |		21		  |
| 1008				 |		68		  |
| 1010				 |		126.125   |
| 1019				 |		976		  |
| 1020				 |		540		  |
| 1097				 |		754		  |
| 1107				 |		520		  |
| 1117				 |		520		  |
| 1127				 |		1573	  |


!!! tip
	N'oubliez pas, vous ne pouvez pas utiliser les message BeiDou 1127 et GLONASS 1010.

Voici quelques information à propos de chacun des messages issus du standard RTCM 10403.3 (Radio Technical Commission for Maritime Services, 2016):

- **Message Type 1002** supporte le fonctionnement RTK mono-fréquence et inclut une indication du rapport porteuse-sur-bruit (carrier-to-noise ratio ou CNR en anglais) pour le satellite GPS, comme mesuré par la station de référence.
- **Message Type 1006** fournit les coordonnées ECEF (earth-centered, earth-fixed) de l'antenne du point de référence (antenna reference point ou ARP en anglais) pour une station de référence et la hauteur de l'ARP au dessus du point de relevé.
- **Message Type 1008** fourni une description ASCII de l'antenne de la station de référence ainsi que le numéro de série de l'antenne, ce qui permet de lever toute ambiguïté sur le numéro de modèle ou lot de production.
- **Message Type 1010** supporte le fonctionnement RTK mono-fréquence et inclut une indication du rapport porteuse-sur-bruit (carrier-to-noise ratio ou CNR en anglais) pour le satellite GLONASS, comme mesuré par la station de référence.
- **Message Type 1019** contient les informations sur les éphémérides du satellite GPS. *This message could be broadcast in the event that the IODC (Issue of Data, Clock) does not match the IODE (Issue of Data, Ephemeris), which would require the differential reference station to base corrections on the previous good satellite ephemeris. This would allow the user equipment just entering the differential system to utilize the corrections being broadcast for that ephemeris, and would support the use of the satellite for differential navigation despite the fact that the satellite ephemeris was in error. It is anticipated that this message type would be broadcast every 2 minutes or so while this condition persisted.
Another use of the message is to assist user receivers to quickly acquire satellites. For example, if the user receiver has access to a wireless service with this message, rather than waiting until one satellite has been acquired and its almanac data processed, it can utilize the ephemeris information immediately.*
- **Message Type 1020** contient les informations sur les éphémérides du satellite GLONASS et possède les mêmes caractéristiques que le message 1019.
- **Messages 1097 (GALILEO), 1107 (SBAS), 1117 (QZSS), 1127 (BeiDou)** sont des messages MSM7 (Multiple Signal Messages). MSM7 sont des messages de haute précision ce qui siginifie qu'ils contiennent l'ensemble complet des observations RINEX avec résolution étendue: *Full GNSS Pseudoranges, Phase Ranges, Phase Range Rate and CNR (high resolution). Key features of the messages are as follows: Effective identification of satellites and their signals by introducing satellite and signal masks, Effective bit consumption for ‘transition GNSS periods’ by introducing cell masks, Effective decomposition of observables by introducing the rough/fine range concept, Effective scalability of different observables by introducing observation blocks, Expressing complete set of RINEX observations for all bands and all signals in the same units (milliseconds).*

	!!! note
		*One of the most important data fields (DF) in MSM messages is the signal mask. It is a bitset indicating which signals from a given GNSS are available from at least one of the multitude of tracked satellites. Each bit in the signal mask is representative of a specific GNSS signal. The definition of the signal mask bits is different for each GNSS, and is provided for each GNSS separately.*

> <cite> Radio Technical Commission for Maritime Services. 2016. RTCM STANDARD 10403.3 DIFFERENTIAL GNSS (GLOBAL NAVIGATION SATELLITE SYSTEMS) SERVICES – VERSION 3. Virginia: Radio Technical Commission for Maritime Services, pp. 108-262</cite>


## Base position

<p style="text-align:center"><img src="../img/reachview/base_mode/position.png" style="width: 800px;"/></p>

There are two main options how to specify base station position. Note that RTK positioning is relative to the base station, so any inaccuracy in it’s position will result in a constant shift of rover coordinates. For many applications it is not critical and averaged single coordinate of the base could be used. If your application requires absolute accuracy for rover position an accurate  base coordinate must be entered.

### Manual
In this mode you supply an a priori known coordinate by locating the unit above surveyed point. Coordinate has to be supplied in ECEF XYZ or in WGS84 Latitude and Longitude and WGS84 ellipsoid height. Antenna height offset is entered at this stage as well, offset is limited to 6.5535 m by the RTCM message.

### Average
By default Reach will average base position every time it starts. This feature significantly simplifies initial setup in a new location, however it will not provide an accurate absolute coordinate.

ReachView has a unique feature that allows it to determine base station position while working as a rover from another base. This is done by obtaining RTK Fixed solution, averaging it over a period of time and this way obtaining an accurate position for the base. A typical scenario would involve setting up a local base station by determining its coordinate from NTRIP and then broadcasting correction locally, thus reducing the baseline for rovers and improving positioning performance.

If the reference station is too far away it is possible to average float and still improve the accuracy of the position.

In case no correction is available when setting up base or absolute accuracy is not required averaged single coordinates could be used.

**Save averaged position to manual**  
After you have successfully obtained averaged position you might want to save it for future use. Click on the “save coordinates” icon and position will be saved as if it was entered in manual mode. Now every time Reach starts it will broadcast this position in correction messages.

**Repeat averaging**  
If you would like to restart base position averaging process you can click on “repeat averaging” icon.This is especially useful in a situation when you accidentally moved Reach during averaging.
