# Compte rendu
## Exercice 2

### Manuel
1) Pour déterminer l'utilité de la commande _which_, j'ai utilisé le manuel de la façon suivante : ```man which```

2) Pour chercher le mot "option", on utilise la commande ```/option```

3) On quitte en utilisant la commande "q"

4) Pour afficher la première page de la section 6 du manuel, on tape ```man 6 intro``` et on obtient l'information selon laquelle cette section concerne les jeux.

### Navigation dans l'arborescence des fichiers
1) Pour aller dans /var/log, on tape ```cd /var/log```.

2) Pour remonter dans /var avec un chemin relatif, on utilisera ```cd ..```

3) Pour remonter dans le fichier personnel on utilise à nouveau ```cd ..```

4) Pour revenir dans /var on fera ```cd /var```

5) L'accès au dossier root est refusé.

6) La commande n'existe pas. ```cd``` n'est pas un programme mais une commande intégrée et sudo ne s'applique qu'aux programmes.

7) Pour arriver à cette arborescence, on tape les commandes suivantes:
```
sudo mkdir dossier1
sudo mkdir dossier2
sudo touch dossier1/fichier1
mkdir dossier2/dossier2.1
mkdir dossier2/dossier2.2
touch dossier2.2/fichier2
touch dossier2.2/fichier3
```

8) On peut supprimer fichier1 (en utilisant sudo) mais pas dossier1 car la commande utilisée pour supprimer un dossier n'est pas celle-ci.

9) Pour supprimer un répertoire, on utilise ```rmdir```.

10) On ne peut pas supprimer ce répertoire car il n'est pas vide.

11) Pour supprimer récursivement ce dossier, on peut utiliser ```rm -rf dossier2```

### Commandes importantes

1) Pour afficher l'heure, on utilise ```date```. La commande time est utilisée conjointement avec une autre "commande" et permet d'afficher les ressources utilisée par cette "commande".

2) Les fichier commençant par un point sont des fichiers cachés.

3) Le programme ls est situé dans le répertoire /usr/bin

4) Grâce à la commande ```alias ll```, on sait que ll est un alias de ```ls -alF``` qui permet d'afficher tous les fichiers, même cachés, d'afficher des informations sur eux ainsi qu'un caractère qui permet d'identifier leur type.

5) La commande ```ls /bin``` permet d'afficher les fichiers contenus dans le dossier /bin

6) ```ls ..``` permet d'afficher les fichiers présents dans le répertoire parent du répertoire courant.

7) La commande ```pwd``` donne le chemin complet du répertoire courant.

8) Cette commande va écrire "yo" dans le fichier plop.

9) Cette commande va écrire "yoyo" dans le fichier plop.

10) ``file`` détermine le type d'un fichier (indépendamment de son type de fichier)

11) Lorsque l'on modifie le contenu de toto, le contenu de titi s'adapte pour y être égal. Lorsque l'on supprime toto, titi garde la dernière valeur de toto.

12) Le fichier titi modifie aussi le fichier **tutu** et inversement. Si on supprime titi, tutu est supprimé conjointement.

13) ```Ctrl + c``` permet d'interrompre le processus.

14) Pour afficher ces informations, on utilisera les commandes suivantes.
    - ```head -5 /var/log/syslog```
    - ```tail -n 5 /var/log/syslog```
    - ```head -n 20 /var/log/syslog | tail -n 11```

15) dmesg est utilisé pour examiner ou contrôler le tampon des messages du noyau, grâce à less, on peut parcourir tous ces messages comme un fichier.

16) Le fichier /etc/passwd contient toutes les informations relatives aux utilisateurs.
Probablement ```man /etc/passwd``` pour afficher les informations du manuel sur ce fichier.

17) Pour afficher seulement la première colonne triée par ordre alphabétique inverse, on utilisera la commande :
```sort -r /etc/passwd | cut -d : -f 1```. Cette commande permet de trier d'abord les informations par ordre inverse puis découpe seulement la première colonne délimitée par ":".

18) Pour avoir le nombre d'utilisateur sous linux, on peut utiliser la commande :
```grep "/bin/bash" /etc/passwd | wc -l```. Cette commande recherche compte le nombre de fois où est mentionnée la chaîne "/bin/bash" qui est associée à un utilisateur unique.

19) Pour trouver le nombre de pages du manuel contenant le mot "conversion", on utilisera la commande ```apropos conversion | wc -l```

20) Pour afficher tous les fichers se nommant "passwd", on se place d'abord à la racine avec ```cd /``` puis on utilise la commande ```find -name passwd```.

21) ```find -name passwd >~/list_passwd_files.txt 2>/dev/null``` liste les résultats trouvés dans le fichier "list_passwd_files.txt" et écrit les erreurs dans le fichier "/dev/null"

22) Il faudra aller chercher dans le fichier où sont définis les alias, on utilisera donc la commande ```grep ll .bashrc``` qui permet de trouver où est défini l'alias ```ll```. 

23) Le fichier "history.log" se trouve dans le répertoire "/var/log/apt/"

24) ```locate``` utilise une base de données indexées listant tous les répertoires dans "/var/lib/mlocate/mlocate.dba". Le fichier "/etc/cron.daily/mlocate" lance l'indexation une seule fois par jour, le fichier tout juste créé n'étant pas indexé, locate ne peut pas le trouver.







