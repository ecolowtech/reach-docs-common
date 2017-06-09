## Quand reprogrammer le firmware

Sur cette page vous trouverez les informtions sur comment reprogrammer le firmware du module Reach.
Veuillez noter que vous n'avez pas besoin de faire cela à moins que vous voulez restaurer le module Reach à un état antérieur ou si une nouvelle version de l'image du firmware est mise à disposition. Si votre module Reach a la version 0.4.9 de ReachView il est nécessaire de le reprogrammer avec la nouvelle image firmware pour recevoir les mises à jour et du support.

La plupart des fonctionnalités sont mises à disposition par l'application ReachView qui peut être mise à jour simplement en appuyant sur le bouton "Update" de l'interface.
!!! note ""
    Plus d'informations sur comment mettre à jour l'application ReachView est disponible dans la [section d'introduction](/#updating).

### Téléchargement du firmware Emlid Reach RTK

Vous pouvez obtenir la dernière version ici:

[**Reach Image v2.3**](https://files.emlid.com/images/ReachImage_v2.3.zip)

Il existe deux possibilités pour reprogrammer l'image. L'outil de configuration basé sur Intel Edion (Intel's Edison Board Configuration Tool) ou un script CLI (Command Line Interface).

## Procédure de programmation

### Guide GUI (avec Interface Graphique)

#### Télécharger l'outil "Intel Edison Board Configuration Tool"

L'outil est [ici](https://software.intel.com/en-us/iot/hardware/edison/downloads). Il est disponible pour Windows, Mac et Linux.

#### Programmation du Reach

- Brancher le module Reach à cet ordinateur
- Décompresser l'image
- Démarrer l'outil "Intel Edison Board Configuration Tool". Appuyez sur suivant **Next**.

<p style="text-align:center" ><img src="../img/reachview/firmware-reflashing/welcome.png" style="width: 800px;" /></p>

- Lire la license, en accepter les termes et appuyer sur **Next** deux fois

<p style="text-align:center" ><img src="../img/reachview/firmware-reflashing/license.png" style="width: 800px;" /></p>


- Installer les drivers (**Pour Windows seulement**)

<p style="text-align:center" ><img src="../img/reachview/firmware-reflashing/setupopt.png" style="width: 800px;" /></p>


- Après l'installation appuyez sur **Flash Firmware**

<p style="text-align:center" ><img src="../img/reachview/firmware-reflashing/setup_with_drivers.png" style="width: 800px;" /></p>

- Choisissez le deuxième éléments: **Use existing image, located at:**  
- Choisissez le chemin vers l'image décompressée (Vous devez pointer vers un ficher **.json** pour Windows et **.hddimg** pour Linux)  
- Appuyez sur **Next** deux fois

<p style="text-align:center" ><img src="../img/reachview/firmware-reflashing/choose_img.png" style="width: 800px;" /></p>

- Poursuivre à la section "Après la programmation"

### Guide avec le Terminal

#### Windows

Avant la programmation:

* Installer les [drivers Intel Edison](http://downloadmirror.intel.com/24909/eng/IntelEdisonDriverSetup1.2.1.exe)
* Décompresser l'image téléchargée
* Déconnecter le module Reach s'il est connecté

Pour programmer:

1. `cd` dans le répertoire de l'image
2. Executer `flashall.bat`
3. Connecter le module Reach
4. Suivre la progression dans la fenêre du terminal
5. Poursuivre à la section "Après la programmation"

#### Mac OS X

Avant la programmation:

* Décompresser l'image téléchargée
* Installer **[homebrew](http://brew.sh)**
* Installer les dépendances avec`brew install dfu-util coreutils gnu-getopt`
* Déconnecter le module Reach s'il est connecté

Pour programmer:

1. `cd` dans le répertoire de l'image
2. Executer `sudo ./flashall.sh`
3. Connecter le module Reach
4. Suivre la progression dans la fenêre du terminal
5. Poursuivre à la section "Après la programmation"

#### Linux

Avant la programmation:

* Décompresser l'image téléchargée
* Déconnecter le module Reach s'il est connecté

To flash:

1. `cd` dans le répertoire de l'image
2. Executer `sudo ./flashall.sh`
3. Connecter le module Reach
4. Suivre la progression dans la fenêre du terminal
5. Poursuivre à la section "Après la programmation"

## Après la programmation

Une fois la première étape de programmation effectuée, le module Reach va redémarrer. **Ne le déconnectez pas avant la fin du redémarrage ou avant qu'il est terminé le processus de configuration**.

Dpeuis la version **1.2** de l'image, les signaux de la LED sur le module Reach pendant le démarrage sont les suivants:

* <font color="magenta">Magenta</font> pendant le démarrage de l'appareil
* Eteint, puis Blanc pendant une seconde pour signifier le démarrage du script
* Clignottement <font color="yellow" style="background-color: grey;">Jaune</font> lors de la recherche de réseaux connus.
* <font color="green">Vert</font> après la création du hotspot
