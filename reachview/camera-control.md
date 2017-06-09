Le module Reach est capable de déclencher une caméra et aussi d'enregistrer des évènements. La fonctionnalité de marquage d'évenements (event mark) est impérative pour la cartographie aérienne parce qu'elle permet d'enregistrer précisément l'heure à laquelle l'obturateur a été activée.

<p style="text-align:center" ><img src="../img/reachview/camera_control/camera.png" style="width: 800px;" /></p>

### Déclencheur de la caméra (Camera trigger)
Le déclencheur de la caméra est seulement disponible pour le module Reach et n'est pas disponible avec le Reach RS. En ajustant les paramètres de cycle de travail (duty cycle) et l'interval (period) vous pouvez adapter les paramètres nécessaires au déclenchement de votre camera. Le graphique temps réel du signal est affiché sur la même page. Notez que cette fonctionnalité n'est pas nécessaire si votre module d'auto-pilotage est capable de déclencher la caméra, surtout qu'il dispose de plus d'informations sur le plan de vol et peut ainsi prendre des décisions éclairées concernant l'instant où la caméra doit être déclenchée.

### Evènements caméra (Camera events)
L'heure du dernier évènement s'affiche pour le déboggage en temps réel. Cela fonctionne seulement avec les satellites GNSS visibles pour la synchronisation temporelle. Un évènement est déclenchée en mettant à la masse la broche de marquage temporel, habituellement par le sabot de l'appareil. Toutes les marques d'évènements sont enregistrées dans les données brutes des logs. La broche de marquage temporel (time mark pin) est conçue pour être connectée à un cable de synchronisation sans aucun composant électronique supplémentaire comme des résistances ou des condensateurs.
