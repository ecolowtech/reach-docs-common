ReachView supporte quatre flux de logs simultanés. Le comportant lorsque la mémoire est pleine ou le découpage des logs peut être spécifié dans les [paramètres](settings/). Chaque flux de log peut être activé ou désactivé, une fois activé les logs continuent à être écrits même après un redémarrage de l'appareil. Après un redémarrage des nouveaux fichiers de logs sont créés automatiquement.

### Données brutes (Raw data)

<p style="text-align:center" ><img src="../img/reachview/logging/raw.png" style="width: 800px;" /></p>

Les donnée brutes sont enregistrées au format UBX, qui peut être convertit en Rinex après téléchargement en utilisant l'utilitaire RTKCONV. Les marques temporelles sont aussi enregistrées dans ce fichier.

### Position

<p style="text-align:center" ><img src="../img/reachview/logging/position.png" style="width: 800px;" /></p>

Les coordonnées peuvent être enregistrées sous différents formats.

**LLH**  
Format texte simplifié pour la Latitude, Longitude et Altitude ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

**XYZ**  
Format texte simplifié pour les coordonnées X, Y, Z ECEF ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

**ENU**  
Format texte simplifié pour les composantes Est (East), Nord (North) et Haut (UP) du référentiel ainsi que le statut de la solution. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

**NMEA 0183**  
Le format standard le plus répandu du secteur. Messages supportés: GPRMC, GPGGA, GPGSA, GLGSA, GAGSA,  GPGSV, GLGSV et GAGSV. La définition du format se situe dans le [manuel RTKLIB ver. 2.4.2](http://www.rtklib.com/prog/manual_2.4.2.pdf) à la page 102.

**ERB**  
Utilisé pour la communcation avec Ardupilot, la description du format se situe [ici](https://files.emlid.com/ERB.pdf).

### Correction de la station fixe (Base correction)

<p style="text-align:center" ><img src="../img/reachview/logging/base_correction.png" style="width: 800px;" /></p>

Les logs de correction provenant de la station fixe (base). Le format est défini en fonction de l'onglet de corrections en entrée "correction input".

### Correction supplémentaire (Additional correction)

<p style="text-align:center" ><img src="../img/reachview/logging/additional.png" style="width: 800px;" /></p>

Les logs provenant de la correction supplémentaire.Le format est défini en fonction de l'onglet de corrections en entrée "correction input".
