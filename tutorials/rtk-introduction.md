### Qu'est-ce qu'un module Reach, quel est son usage ?

Le module Reach est un récepteur RTK GNSS pour les applications où votre GPS standard avec sa précision de plusieurs mètres ne suffit pas. Il repose sur la technology RTK (cinématique temps réel ou real-time kinematic en anglais) pour fournir une précision de l'ordre du centimètre.

Le RTK existe depuis longtemps, mais jusqu'alors utilisé principalement par des arpenteurs-géomètres et inacessible aux amateurs ou makers. Si vous aviez besoin d'une précision de quelques centimètres il vous fallait débourser plusieurs milliers d'euros dans un système RTK. Avec le module Reach nous voulons changer cela.

Le module Reach s'appuie sur un logiciel de traitement RTK open-source appelé RTKLIB écrit par Tomoji Takasu. Auparavant un ordinateur était nécessaire pour faire tourner RTKLIB, mais désormais toutes les fonctionnalités de RTKLIB sont disponibles directement au sein du module Reach.

### Qu'est-ce que le RTK ?

Le RTK est une technique utilisé pour améliorer l'exactitude d'un système GPS. Les récepteurs GPS usuels, comme ceux que vous avez dans votre smartphone, ou dans la plupart de la robotique peuvent seulement déterminer leur position avec une précision de 2 à 4 mètres. En RTK vous pouvez obtenir une précision de quelques centimètres.

L'ensemble du système GPS repose sur la mesure de la durée du parcours d'un signal transmis depuis un satellite jusqu'au récepteur. En connaissant les orbites précises des engins spatiaux - les éphémérides, et au moins 4 durée de parcours il est possible de calculer sa position sur la planète.
Avec la fréquence porteuse GPS L1 de 1575Mhz, la longueur d'onde est d'environ 19cm. Un récepteur mesure également la phase de la porteuse de chacun des signaux. Théoriquement, cela pourrait donner une précision de l'ordre du millimètre, alors pourquoi avons-nous toujours à nous contenter d'une précision de 2 à 4 mètres ? Quelles sont les sources d'erreurs, et que pouvons-nous faire pour nous en affranchir ?

Les satellites sont en orbite à environ 20 200 km de la surface de la Terre. Les signaux transmis traversent la ionosphère et l'atmosphère et sont ralentis ou perturbés sur leur trajet. Par exemple, le temps de transmission entre un jour nuageux ou ensoleillé est différent ! Beaucoup de facteurs peuvent augmenter l'erreur sur la position, la bonne nouvelle c'est qu'on peut considérer que ces facteurs ne changent que très peu sur une zone donnée.

C'est ce que font les systèmes d'augmentation GPS (DGPS), comme SBAS ou WAAS qui mesurent les perturbations instantanées des signaux au niveau de nombreuses stations de contrôle au sol à travers le monde, élaborent un modèle des erreurs de propagation et transmettent les corrections par satellite ou radio. Beaucoup de récepteurs commerciaux peuvent utiliser ces signaux pour obtenir une précision inférieure au mètre. Mais comment faire si on veut plutôt s'approcher du centimètre ?

La technologie qui nous permet de faire cela est appelée RTK (cinématique temps réel ou real-time kinematics en anglais). Deux récepteurs sont utilisés, l'un d'eux est stationnaire et est appelé "station fixe" (base station en anglais), et l'autre est le "récepteur mobile" (rover en anglais). La station fixe mesure les erreurs, et sachant qu'elle est fixe, transmet les corrections au récepteur mobile (rover). L'idée est simple, mais pas les mathématiques. Les systèmes commerciaux peuvent être plus précis que le centimètre et coûtent une fortune ($5k+).

Aussi, si vous n'avez pas besoin d'avoir les coordonnées précises en temps réel, vous pouvez simplement enregistrer les données du récepteur mobile (rover) et de la station fixe (base) et effectuer un traitement dans un second temps ce qui permet d'éliminer la nécessité d'un lien radio continu. Cette méthode est appelée le post-traitement (post-processing en anglais) et c'est la méthode la plus précise de toute.

** Comparaison de coordonnées en mode RTK ou autonome **

*Mode statique (Static mode):*

<p style="text-align:center" ><img src="../img/reach/rtk-introduction/reach-static-rtk-demo.png" style="width: 800px;" /></p>

*Mode cinématique (Kinematic mode):*

<p style="text-align:center" ><img src="../img/reach/rtk-introduction/reach-kinematic-rtk-demo.png" style="width: 800px;" /></p>
