
### Formats

<p style="text-align:center" ><img src="../img/reachview/position_output/format.png" style="width: 800px;" /></p>

Le module Reach supporte les formats de sortie suivants pour les coordonnées:

#### LLH
Format texte simplifié pour la Latitude, Longitude et Altitude ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

#### XYZ
Format texte simplifié pour les coordonnées X, Y, Z ECEF ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

#### ENU
Format texte simplifié pour les composantes Est (East), Nord (North) et Haut (UP) du référentiel ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

#### NMEA 0183
Le format standard le plus répandu du secteur. Messages supportés: GPRMC, GPGGA, GPGSA, GLGSA, GAGSA,  GPGSV, GLGSV et GAGSV. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

#### ERB
Utilisé pour la communcation avec Ardupilot, la description du format se situe [ici](https://files.emlid.com/ERB.pdf).


**Les données dans chacun de ces formats peuvent être envoyées par laison série (Serial), TCP, ou Bluetooth.**

### Laison Série (Serial)
La connexion au port série est disponible avec différentes options de connexion matérielle. Toutes supportent les vitesses de transmission suivantes: 4800, 9600, 14400, 19200, 28800, 38400, 56000, 57600, 115200, 128000, 153600, 230400, 256000, 460800, 921600

#### UART
Correspond à l'UART TTL du module Reach ou le port RS232 du connecteur d'extension disponible sur le Reach RS. C'est un cas usuel que d'y connecter l'auto-pilotage ou une autre consommateur des données de position.

#### USB-to-PC
Quand le module Reach est connecté à un ordinateur via USB il sera visible en tant que différents appareils, l'un d'entre eux est via un port série. Vous pouvez utiliser ce port série pour envoyer les données de correction à l'ordinateur.

#### USB OTG
Utiliser un cable micro-USB OTG pour connecter des accessoires USB. Dans ce mode là seulement les appareils USB qui émulent un port série peuvent être utilisés. Exemples de puces répandues qui sont supportées : FT232, CP2102. Il y a de nombreux appareils basés sur ces puces qui peuvent vous fournir un UART TTL ou un port RS232.

### TCP
Un scénario typique pour utiliser TCP est d'envoyer les données de positionnement sur le même réseau ou sur un serveur avec une adresse ip publique.

Le protocol TCP fonctionne avec deux modes:

#### Serveur
Vous devez renseigner le port et ensuite les clients seront en mesure de se connecter à cet appareil sur son adresse IP. Plusieurs clients peuvent se connecter au même serveur.

#### Client
Vous devez renseigner l'adresse IP et le numéro du port du serveur.

Si ReachView ne permet pas de renseigner un port spécifique, cela signifie qu'il est utilisé pour un usage interne.

### Bluetooth
La sortie Bluetooth est utilisé pour transmettre de manière continue les données de position à des smartphones, tablettes ou collecteurs de données. Veuillez vérifier que votre appareil est associé dans les paramètres Bluetooth.
