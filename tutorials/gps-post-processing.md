## Données requises

Ce tutoriel nécessite:

* Les logs brutes du récepteur mobile (rover)
* Les logs brutes de la station fixe (base)
* (en option) Pour une précision absolue: les logs des observations RINEX d'une station de référence distante de moins de 100km
* (en option) Pour améliorer la précision du traitement: les fichiers d'éphéméridese et d'horloges précises issus de l'IGS

Le parcours du récepteur mobile est calculé en position relative à la station fixe (base) donc pour avoir le parcours du récepteur mobile (rover) avec des coordonnées en précision absolue la position exacte de la station fixe (base) doit être connue. Il faut soit positionner la station fixe en un point de coordonnées connues ou les déterminer avec un post-traitement utilisant une station de référence et en étant en mode statique. Il est préférable que la station de référence soit dans un rayon de 100 km, mais un rayon plus important peut aussi fonctionner.


## Convertir les logs brutes en RINEX

Démarrer [RTKLIB RTKCONV](https://files.emlid.com/RTKLIB/rtkconv_emlid_b27.exe) après avoir télécharger les fichiers brutes depuis le module Reach sur votre PC.

* Ajouter les logs brutes du récepteur mobile (rover) dans le premier champ et sélectionner le répertoire de sortie.
* Sélectionner le format de votre log dans le menu déroulant. Choisissez le format u-blox si les logs ont été téléchargés depuis chacun des appareils. Sinon, choisissez RTCM3 si les logs de la station fixe (base) et du récepteur mobile (rover) ont été récupérés depuis le récepteur mobile (rover).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkconv_format.png" style="width: 600px;"></div>

* Cliquez sur le bouton "Options".
* Choisissez "RINEX Version" 3.03.
* Activez les systèmes satellites "Satellites Systems" dont vous avez besoin.
* Appuyez sur "OK" et ensuite sur convertir "Convert".

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkconv_options.png" style="width: 600px;"></div>

Maintenant vous pouvez répétez l'opération avec les logs de la station fixe. Mais n'oubliez pas de changer de format.
Après cette étape votre répertoire de sortir ressemblera à ça.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkconv_output_folder.png" style="width: 600px;"></div>


### Déterminer les coordonnées de la station fixe (base)

Démarrer le logiciel [RTKLIB RTKPOST](https://files.emlid.com/RTKLIB/rtkpost_emlid_b27.exe) et remplissez les champs comme indiqué ici. Si vous le démarrez pour la première fois vous avez besoin de définir le mode statique (Static) ou cinématique (Kinematic) dans les options pour débloquer les champs correspondant aux données de la station fixe (base). Vous pouvez ignorer l'heure de départ (start time), ce n'est pas obligatoire.

* Sélectionner le fichier .obs du champs du récepteur mobile, le "rover". (Fichier RINEX issu du récepteur mobile, le "rover" en anglais)
* Sélectionner le fichier .obs du champs de la station fixe, la "base". (Fichier RINEX issu de la station fixe, la "base" en anglais)
* Sélectionner le fichier .nav de la station fixe (base) ou du récepteur mobile (rover) dans le troisième champ.
* (en option) Vous pouvez aussi lors de cette étape ajouter les éphémérides et horloges précises. Elles sont requises pour les grandes distances au référentiel (long baselines).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_adding_files.png" style="width: 600px;"></div>


Poursuivez ensuite en appuyant sur le bouton "Options".

* Sélectionnez le mode de positionnement "positioning mode" souhaité. Souvent cinématique (Kinematic) ou statique (static).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_setting1_mode.png" style="width: 600px;"></div>


* Choisissez une valeur du masque d'élevation "Elevation Mask". Souvent entre 15 et 20 degrés.
* Appuyez sur le bouton concernant le masque du rapport signal-bruit "SNR Mask" et spécifier une valeur. Cela permettra de ne pas tenir compte des satellites avec des intensités de signaux trop faibles.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_setting1_mask.png" style="width: 600px;"></div>


* Activez "Rec Dynamics" pour estimer la vitesse et l'accélération du récepteur mobile. À utiliser pour un usage différentiel DGPS/DGNSS ou les modes cinématiques (kinematic).
* Sélectionner les systèmes de navigation (navigation systems).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_setting1_dynamics.png" style="width: 600px;"></div>


* Ouvrez l'onglet "Settings2".
* Paramétrez la résolution de l'ambiguïté à l'entier adéquat "Integer Ambiguity Res" à la valeur "Fix and Hold". Dans ce mode les ambiguïtés sont estimées et résolues en continu. Si la validation est OK, les ambiguïtés à l'entier adéquat sont fortement contraintes vers les valeurs calculées.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_setting2_ambiguity.png" style="width: 600px;"></div>


* Spécifiez une valeur pour la variation maximale de la position liée à la résolution d'ambiguïté "Max Pos Var for AR" et activez le filtre de résolution d'ambiguïté "AR Filter" à droite.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_setting2_ar.png" style="width: 600px;"></div>


* Passez à l'onglet "Positions"..
* Sélectionnez la station fixe "Base Station". Choisissez le moyennage de la position avec une solution SINGLE "Average of Single Position" en s'appuyant sur un fichier de log ou utilisez la position située dans l'en tête du fichier RINEX avec "RINEX Header Position" qui se basera sur l'en-tête du fichier .obs.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_positions_base.png" style="width: 600px;"></div>


* Appuyez sur le bouton "OK" puis lancer le traitement avec "Execute" dans la fenêtre principale.
* Vous verrez une barre d'avancement verte. Patientez jusqu'à l'indication de fin "done". Cela peut prendre un temps conséquent si vos fichiers de logs sont volumineux. Dans ce cas la fenêtre ne répond plus à vos actions. Patientez alors tranquillement.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_execute.png" style="width: 600px;"></div>


Une fois terminé vous verrez à peu de choses près les fichiers suivants dans votre répertoire de sortie. Le fichier .pos avec "\__event" contiendra les horodatages (timestamps) si vous en aviez durant votre relevé.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkpost_output_folder.png" style="width: 600px;"></div>

## Visualiser et Analyser les résultats

Ouvrez [RTKLIB RTKPLOT](https://github.com/tomojitakasu/RTKLIB_bin/raw/rtklib_2.4.3/bin/rtkplot.exe) et glissez-déposez votre fichier ".pos".
Si vous voyez des points verts cela signifie que la solution est FIX (Q=1), orange signifie FLOAT (Q=2) et rouge signifie SINGLE (Q=5).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkplot_pos.png" style="width: 600px;"></div>


Ensuite vous pouvez ajouter votre fichier ".obs" pour obtenir plus d'outils d'analyse dans le menu déroulant.
Par exemple, la première image affiche les visibilités satellites "Satellite Visibility" et la seconde la "Position" selon les 3 axes.

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkplot_satvis.png" style="width: 600px;"></div>

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkplot_position.png" style="width: 600px;"></div>

Si vous avez des marques temporelles vous pouvez les ajouter en tant que Solution-2 (File -> Open Solution2).

<div style="text-align: center;"><img src="../img/reach/post-processing/rtkplot_timemarks.png" style="width: 600px;"></div>

Pas mal, non ?

Tous les droits des fichiers de logs sont la propriétés de notre bon ami et excellent arpenteur Luke Wijnberg.

Pour plus d'informations concernant les options de traitement, consultez le [manuel RTKLIB](http://www.rtklib.com/prog/manual_2.4.2.pdf).

<!--

Maintenant changez d'onglet et activez la résolution d'ambiguïté GPS à "Fix-and-hold" et désactivez la pour Glonass en la mettant à "OFF". La résolution d'ambiguïté Glonass peut être activée si la station fixe (base) et le récepteur mobile (rover) sont tous les deux des modules Reach.

![image](img/post-processing/Post3.PNG)

Le fichier RINEX des observations de la station de référence inclut la position exacte dans l'en-tête du fichier, donc nous l'utiliserons pour la position de la station fixe (base). Ceci est vraiment important parce qu'il s'agit des coordonnées de références utilisées dans toute la procédure de post-traitement. Vous avez besoin d'un point connu à partir duquel vous baser.

![image](img/post-processing/Post4.PNG)

Vous pouvez maintenant cliquez sur "Execute" and vérifiez la qualité de la solution, Q=1 signifie FIX.

![image](img/post-processing/Post5.PNG)

Une fois les calculs terminés cliquez sur le bouton de création du graphique "Plot" pour afficher le tracé. Nous obtenons les coordonnées de la station fixe (base), enregistez-là nous allons l'utiliser dans l'étape suivante.

![image](img/post-processing/POst6.PNG)

### Calculer le tracé du récepteur mobile (rover)

Parcourez votre disque jusqu'aux fichiers Rinex ".obs" de votre récepteur mobile (rover), ".obs" de votre station de référence (base) et fichier de navigation ".nav" issue de votre station fixe (base).

![image](img/post-processing/Post7.PNG)

Poursuivez dans les options et sélectionner le mode de positionnement "cinématique", pour indiquer à RTKLIB que le récepteur mobile était en mouvement. Sélectionner les systèmes de navigation et les options des filtres. Activez également le filtre dynamique "Rec Dynamics".

![image](img/post-processing/Post8.PNG)

Dans ce cas la résolution d'ambiguïté Glonass peut être activé à "ON", puisque les deux modules sont identiques.

![image](img/post-processing/Post9.PNG)

Nous arrivons alors à l'étape où nous avons besoin d'entrer les coordonnées de la station fixe (base) que nous avons calculés lors d'une étape précédente.

![image](img/post-processing/Post10.PNG)

Cliquez sur "Execute" puis affichez le résultat avec "Plot". Pas mal, mais certaines zones sont jaunes ce qui indique une solution FLOAT. Nous pouvons analyser les observations pour essayer de trouver la source du problème.

![image](img/post-processing/Post11.PNG)

Dans RTKPLOT allez dans file-> open observations et sélectionner le fichier d'observations du récepteur mobile (rover). Changez la vue pour afficher les visibilités satellites. Il se peut que vous ayez besoin d'aller dans les options de la vue et de sélectionner tous les systems de navigations "ALL" et de paramétrer l'option de saut de cycle "cycle slip" à "LLI flat" pour voir les données comme indiqué dans la figure. On peut remarquer que la réception est moins bonne au début, et nous pouvons donc les éliminer pour éviter que les filtres utilisent des données de mauvaise qualité.

![image](img/post-processing/Post12.PNG)

En affichant la vue "Position" il est évident que le décollage s'opère vers 14h05 et qu'ensuite la réception est bien meilleure.

![image](img/post-processing/Post13.PNG)

Relançons le post-traitement à nouveau, mais en supprimant les données avant 14h03.

![image](img/post-processing/Post14.PNG)

C'est bien mieux maintenant !

![image](img/post-processing/Post15.PNG)

Et qu'aurait-il pu se passer si nous n'avions pas utilisé la position exacte de la station fixe (base), mais simplement une solution SINGLE moyennée ? La figure affiche un zoom sur trois virages, où le tracé vert a été calculé en utilisant la position exacte de la station fixe (base), et le tracé bleu a été calculé sans utiliser la position exacte. Les deux tracés sont précis, mais le tracé bleu est décalé de plusieurs mètres.

![image](img/post-processing/Post16.PNG) -->
