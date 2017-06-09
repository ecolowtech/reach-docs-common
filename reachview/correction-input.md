## Correction de la station fixe (Base correction)

Paramétrer les flux de correction est nécessaire si vous voulez allez plus loin qu'une utilisation en mode autonome. Le module Reach support plusieurs formats de correction en entrée: RTCM2, RTCM3, OEM4, OEM3, UBX, SS2, HEMIS, SKYTRAQ, SP3. RTCM3 est le format le plus répandu du secteur. Les données de tous ces formats peuvent être reçues via une liaison série (Serial), TCP, NTRIP ou LoRa avec un Reach RS.

### Liaison Série (Serial)

<p style="text-align:center" ><img src="../img/reachview/correction_input/serial.png" style="width: 800px;" /></p>

La connexion au port série est disponible avec différentes options de connexion matérielle. Toutes supportent les vitesses de transmission suivantes: 4800, 9600, 14400, 19200, 28800, 38400, 56000, 57600, 115200, 128000, 153600, 230400, 256000, 460800, 921600

#### UART
Correspond à l'UART TTL du module Reach ou le port RS232 du connecteur d'extension disponible sur le Reach RS. C'est un cas usuel que d'y connecter la radio pour transmettre les données de correction.

#### USB-to-PC
Quand le module Reach est connecté à un ordinateur via USB il sera visible en tant que différents appareils, l'un d'entre eux est via un port série. Vous pouvez utiliser ce port série pour envoyer les données de correction à l'ordinateur.

#### USB OTG
Utiliser un cable micro-USB OTG pour connecter des accessoires USB. Dans ce mode là seulement les appareils USB qui émulent un port série peuvent être utilisés. Exemples de puces répandues qui sont supportées : FT232, CP2102. Il y a de nombreux appareils basés sur ces puces qui peuvent vous fournir un UART TTL ou un port RS232. C'est aussi une solution simple pour connecter des modems radio.

### NTRIP

<p style="text-align:center" ><img src="../img/reachview/correction_input/ntrip.png" style="width: 800px;" /></p>

NTRIP est la norme du secteur pour transférer les corrections GNSS via Internet, avec ReachView vous pouvez utiliser tout service publique ou votre propre fournisseur privé. NTRIP ne permet pas une communication point à point, par exemple vous ne pouvez pas l'utiliser pour transmettre les corrections d'un module Reach à un autre directement. Dans la terminolgie NTRIP il y a des serveurs, des clients et des diffuseurs. Le serveur envoie les corrections au diffuseur et les clients peuvent les recevoir en se connectant à ce diffuseur.

Pour envoyer des correction à un diffuseur NTRIP vous avez besoin de:

+ l'adresse IP ou nom de domaine du diffuseur
+ port
+ nom d'utilisateur
+ mot de passe
+ point de montage
+ format (souvent RTCM3)

Quand la connexion est effectuée avec un point de montage qui dispose de la fonctionnalité VRS (Station de Référence Virtuel ou Virtual Reference Station) ou de plus proche proximité (Nearest), ce qui vous permet de vous connecter automatiquement à la station fixe la plus proche, il est nécessaire de renvoyer votre position au diffuseur (caster). Cochez alors la case “Send NMEA GGA messages to the corrections provider” et une fois que le module Reach a calculé une solution SINGLE il commencera à l'envoyer au diffuseur (caster).

### TCP

<p style="text-align:center" ><img src="../img/reachview/correction_input/tcp.png" style="width: 800px;" /></p>


Un scénario typique pour utiliser l'entrée TCP pour une correction est quand le station fixe (base) et le récepteur mobile (rover) sont sur le même réseau. Notez que lorsque les appareils sont sur des réseaux différents vous ne pouvez pas transmettre de données directement à moins que les adresses IP publiques soient connues et que les routeurs sont configurés avec une redirection de port. Le protocol TCP peut aussi être utilisé pour envoyer ou recevoir des données depuis un serveur distant avec une IP publique.

Le protocol TCP fonctionne avec deux modes:

#### Serveur
Vous devez renseigner le port et ensuite les clients seront en mesure de se connecter à cet appareil sur son adresse IP. Plusieurs clients peuvent se connecter au même serveur.

#### Client
Vous devez renseigner l'adresse IP et le numéro du port du serveur.

Si ReachView ne permet pas de renseigner un port spécifique, cela signifie qu'il est utilisé pour un usage interne.

### Radio LoRa (seulement Reach RS)

<p style="text-align:center" ><img src="../img/reachview/correction_input/Lora.png" style="width: 800px;" /></p>

Le Reach RS possède un radio LoRa interne qui est utilisée pour recevoir et envoyer les corrections. La radio fonctionne dans un seul sens, elle peut être configurée soit pour envoyer des corrections (depuis la station fixe ou base) ou pour les recevoir (récepteur mobile ou rover). En utilisant la modulation LoRa il est possible d'atteindre une portée de 19km en ligne de visée directe ou de quelques kilomètres en zone urbaine avec seulement 20 dBm de puissance de sortie. Tant que les paramètres de fréquence et de vitesse de transmission correspondent il est possible de connecter un nombre infini de récepteur mobile qui peuvent alors recevoir les corrections depuis une même station fixe (base).

Les vitesses de transmission sur les Reach RS émetteurs (base) et récepteurs (rover) doivent correspondre.

## Correction supplémentaire (Additional correction)
Sera utilisé pour des horloges et éphémérides précises. Pas encore implémenté.

<p style="text-align:center" ><img src="../img/reachview/correction_input/additional.png" style="width: 800px;" /></p>
