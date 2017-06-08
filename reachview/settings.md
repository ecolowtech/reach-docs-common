### Vérifier la version de l'application
À chaque fois que vous allumez le module Reach et le connectez à un réseau Wi-Fi, il vérifiera si une mise à jour ReachView est disponible et vous notifiera en fonction.

<p style="text-align:center" ><img src="../img/reachview/settings/update_check.png" style="width: 800px;" /></p>


Notez que la vérification n'a lieu qu'une fois lors du processus de démarrage. Si vous voulez forcez la vérification d'une nouvelle version veuillez vous rendre sur l'utilitaire de mise à jour ReachView Updater. Il est disponible sur le port 5000, par exemple `http://reach.local:5000`. Il vérifiera automatiquement auprès des serveurs de mises à jour Emlid quand vous ouvrirez la page.

<p style="text-align:center" ><img src="../img/reachview/settings/update_check5000.png" style="width: 350px;" /></p>

### Modifier le nom du module Reach
Le nom du module Reach peut être modifié afin de dissocier différents modules. Un cas d'usage courant est de renommer les appareils selon leur fonction de station fixe (base) ou récepteur mobile (rover). Le nom de l'appareil sert de racine pour le nom du hotspot et du réseau local. Le nom par défaut est "reach", changer ce nom modifiera le nom local `http://reach.local` ainsi que le nom du hotspot `reach:xx:xx`.


<p style="text-align:center" ><img src="../img/reachview/settings/settings.png" style="width: 800px;" /></p>

### Restauration des paramètres par défaut
Cliquez sur le bouton de remise à zéro des paramètres “Reset setting to default” afin de restaurer les paramètres de configuration à ceux de la sortie d'usine. Seulement les logs et paramètres sans fil seront conservés. Si vous souhaitez effectuer une remise à zéro totale comme en sortie d'usine et effacer toutes vos données vous pouvez [reprogrammer le firmware](firmware-reflashing).

### Modifier le mot de passe du hotspot
Le mot de passe par défaut du hotspot est “emlidreach”, vous pouvez le modifier pour des questions de sécurité. Si vous oubliez le mot de passe du hotspot vous pouvez toujours accéder au module Reach en le connectant à un réseau Wi-Fi connu. Si vous avez perdu tout accès au module Reach vous pouvez [reprogrammer le firmware](firmware-reflashing) and le configurer à nouveau.

### Paramètres de journalisation (Logging)
Full memory behaviour
Spécifie comment ReachView gère le problème en cas de mémoire pleine, il peut soit arrêter d'enregistrer dans les logs ou écraser les anciens logs pour permettre d'écrire les nouveaux. Dans la plupart des cas les logs tournants “rolling logs” sont recommandés.

### Interval de découpage des logs
Un nouveau fichier de log sera créé toutes les N heures, tout en préservant les anciens logs aussi. Ce paramètre vous permet de maîtriser la taille des fichiers avec laquelle vous travaillez.
