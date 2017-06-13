## Démonstration Vidéo

Un grand merci pour votre utilisateur professionnel [TB_RTK](https://community.emlid.com/users/tb_rtk/activity) pour l'importante contribution à ce tutoriel.

<div style="text-align: center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/yy8EVSMq9Bk" frameborder="0" allowfullscreen></iframe></div>

Il est possible de remplacer le GPS interne de votre appareil Android, de cette façon toute application utilisation le positionnement du téléphone sera en mesure d'utiliser les coordonnées RTK calculées. Les applications couramment utilisées sont Mobile Topographer Pro et ESRI Arcgis Collector.

## Configuration du module Reach

Pour utiliser un module Reach avec une application Android, vous aurez besoin d'effectuer les étapes suivantes :

* Associer votre appareil Android avec votre module Reach / Reach RS

!!! tip
    Pour cette étape, mettez votre appareil en détectable. Ensuite, allez dans l'onglet **Wifi/Bluetooth** et cherchez votre appareil dans la section Bluetooth. Une fois que votre appareil apparaît dans la section "détectable", cliquez dessus pour envoyer une demande d'association. Accpetez la demande sur votre appareil. Votre appareil apparaît ensuite dans la section des appareils associés "paired devices".


<p style="text-align:center"><img src="../img/reach/mock-location/bluetooth.png" style="width: 800px;"/></p>


* Dans l'onglet "Position output" activiez l'export des coordonnées via Bluetooth "BT" et choisissez le format **NMEA**

!!! tip
    N'oubliez pas d'appliquez les changements effectués sur le récepteur mobile en cliquant sur "Apply"

<p style="text-align:center"><img src="../img/reach/mock-location/solution.png" style="width: 800px;"/></p>

## Positions fictives Android

Nous fournissons un guide d'utilisation du module Reach avec [Lefebure NTRIP caster](https://play.google.com/store/apps/details?id=com.lefebure.ntripclient) réalisé par Lefebure Design.

Malgré l'appellation de diffuseur NTRIP (caster) cette application autorise également les entrées de données NMEA par bluetooth. Aussi, elle supporte la fonctionnalité Android de **Position fictives** (ou "mock location" en anglais), qui permet de remplacer votre récepteur GPS interne intégré dans votre appareil par un appareil externe fournissant ces données de position, le module Reach dans notre cas.

Pour connecter le module Reach, effectuez les étapes suivantes :

* Ouvrir l'application, allez dans les préférences ("settings") en appuyant sur le bouton d'engrenage dans le coin en haut à droite

<p style="text-align:center"><img src="../img/reach/mock-location/lefebure-main-screen.jpg" style="width: 300px;"/></p>

* Allez ensuite dans les paramètres du récepteur "receiver settings"

<p style="text-align:center"><img src="../img/reach/mock-location/lefebure-settings.jpg" style="width: 300px;"/></p>

!!! À Vérifier dans "Receiver Settings":
    1. Modifier l'appareil Bluetooth pour qu'il s'agisse du module Reach auquel vous êtes associé
    2. Modifier la méthode de connexion Bluetooth "Bluetooth Connection Method" à **Secure via Reflection**  
    3. Activez et Autorisez les **Positions Fictives** (ou **Mock location** en anglais) si besoin

<p style="text-align:center"><img src="../img/reach/mock-location/lefebure-receiver-settings.jpg" style="width: 300px;"/></p>

* Retournez à l'écran principal, cliquez sur **Connect** et regarder les informations de connexion!

<p style="text-align:center"><img src="../img/reach/mock-location/lefebure-connected.jpg" style="width: 300px;"/></p>

Désormais les coordonnées de votre appareil Android sont remplacées par les coordonnées du module Reach / Reach RS et vous pouvez les utiliser dans n'importe quelle application.
