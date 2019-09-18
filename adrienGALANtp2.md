# Adrien GALAN - TP2

## 1 - Variables d’environnement

1) Le fichier d'historique des commandes se trouve à la racine du répertoire utilisateur. C'est un fichier caché qui se nomme **.bash_history**
2) La variable **HOME**, qui contient le répertoire personnel de l'utilisateur, permet à la commande **cd** de revenir dans ce dernier sans arguments.
3)  - LANG: détermine la langue que les logiciels
utilisent pour communiquer avec l’utilisateur 
    - PWD: renvoie le chemin courant absolu
    - OLDPWD: renvoie le dernier chemin courant asbolu avant un changement de répertoire
    - SHELL: /bin/bash
4) `MY_VAR="test"` / `echo $MY_VAR` pour vérifier
5) La commande **bash** sert à ouvrir un nouveau shell, la variable **MY_VAR** n'existe donc pas. 
6) `export MY_VAR="test"`, et même en ouvrant un nouveau shell, on retrouve bien notre variable d'environnement.
7) `NOMS="MAGAT"` / `echo $NOMS`
8) La commande `echo "Bonjour à vous deux, $NOMS !"` permet d'afficher le message suivant en remplaçant la variable **NOMS** par son contenue.
9) Si on donne une valeur vide à une variable elle sera toujours présente dans l'environnement, on peux le vérifier grâce à la commande **env**, alors que la commande **unset** permet de supprimer la variable de l'environnement.
10) 

## 2 - Contrôle de mot de passe

```bash
#!/bin/bash
PASSWORD="123test"
read -p "Saisissez votre mot de passe:" -s passUser
if [ $PASSWORD = $passUser ]; then
    echo "Mot de passe valide."
else
    echo "Mot de passe invalide."
fi
```

`chmod u+x testpdw.sh` pour rendre le script executable

## 3 - Expressions rationnelles

```bash
#!/bin/bash
function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

if [ $# = 1 ] ; then
    is_number $1
    echo $?
else
    echo "1 paramètre est nécessaire."
fi
```

## 4 - Contrôle d’utilisateur

```bash
utilisateurs=$(grep "/bin/bash" /etc/passwd | cut -d : -f 5)
utilisateurValide=0
if [ $# = 1 ] ; then
    for utilisateur in $utilisateurs; do
        if [ $1 = $utilisateur ] ; then
            utilisateurValide=1
        fi
    done
    if [ $utilisateurValide = 1 ] ; then
        echo "Utilisateur valide"
    else
        echo "Utilisateur non valide"
    fi
else
    echo "Utilisation: $0 nom_utilisateur"
fi
```

## 5 - Factorielle

```bash
#!/bin/bash
if [ $# = 1 ] ; then
        resultat=1
        compteur=2
        while (( $compteur <= $1 ))
        do
                resultat=$(($resultat * $compteur))
                compteur=$(($compteur+1))
        done
        echo $resultat
else
        echo "Arguments non valide"
fi
```

## 6 - Le juste prix

```bash
#!/bin/bash
nombre=$(($RANDOM*1000/32767))
read -p 'Donner une  première estimation' reponse
while [ $reponse -ne $nombre ]
do
        if [ $reponse -lt $nombre ]
        then
                read -p 'Plus' reponse
        elif [ $reponse -gt $nombre ]
                then
                        read -p 'Moins' reponse
        fi
done
echo 'c est gagne'
```

## 7 - Statistiques

### 1)
```bash
#!/bin/bash
function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

if [ $# = 3 ] ; then
        canContinue=0
        for param in "$@"
        do
                is_number $param
                if [ $? = 1 ] ; then
                        canContinue=1
                fi
                if [ $canContinue = 0 ] ; then
                        if (( param < -100 )) ; then
                                canContinue=1
                        elif (( param > 100 )) ; then
                                canContinue=1
                        fi
                fi
        done
        if [ $canContinue = 0 ] ; then
                min=$1
                for param in "$@"
                do
                        if (( $min > $param )) ; then
                                min=$param
                        fi
                done
                max=$1
                for param in "$@"
                do
                        if (( $max < $param )) ; then
                                max=$param
                        fi
                done
                moyenne=$(( ( $1 + $2 + $3 ) / 3 ))
                echo "Min : $min"
                echo "Max: $max"
                echo "Moyenne: $moyenne"
        else
                echo "Arguments non valide"
        fi
else
        echo "Arguments non valide"
fi
```

### 2)
```bash
#!/bin/bash
function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

canContinue=0
for param in "$@"
do
        is_number $param
        if [ $? = 1 ] ; then
                canContinue=1
        fi
        if [ $canContinue = 0 ] ; then
                if (( param < -100 )) ; then
                        canContinue=1
                elif (( param > 100 )) ; then
                        canContinue=1
                fi
        fi
done
if [ $# = 0 ] ; then
        canContinue=1
fi
if [ $canContinue = 0 ] ; then
        min=$1
        for param in "$@"
        do
                if (( $min > $param )) ; then
                        min=$param
                fi
        done
        max=$1
        for param in "$@"
        do
                if (( $max < $param )) ; then
                        max=$param
                fi
        done
        somme=0
        for param in "$@"
        do
                somme=$(( $somme + $param ))
        done
        moyenne=$(( $somme / $# ))
        echo "Min : $min"
        echo "Max: $max"
        echo "Moyenne: $moyenne"
else
        echo "Arguments non valide"
fi
```

### 3)

```bash
#!/bin/bash
function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

canContinue=0
read -p "1 pour saisir un nombre / 0 pour continuer" decisio
nombres=()
while [ $decisio != 0 ]
do
        read -p "Saisir un nombre" nombre
        nombres+=($nombre)
        read -p "1 pour saisir un nombre / 0 pour continuer" decisio
done
for param in $nombres
do
        is_number $param
        if [ $? = 1 ] ; then
                canContinue=1
        fi
        if [ $canContinue = 0 ] ; then
                if (( param < -100 )) ; then
                        canContinue=1
                elif (( param > 100 )) ; then
                        canContinue=1
                fi
        fi
done
echo $nombres
if [ $canContinue = 0 ] ; then
        min=${#nombres[0]}
        echo $min
        for param in "$nombres"
        do
                if (( $min > $param )) ; then
                        min=$param
                fi
        done
        max=${#nombres[0]}
        for param in "$nombres"
        do
                if (( $max < $param )) ; then
                        max=$param
                fi
        done
        somme=0
        for param in "$nombres"
        do
                somme=$(( $somme + $param ))
        done
        moyenne=$(( $somme / ${#nombres[@]} ))
        echo "Min : $min"
        echo "Max: $max"
        echo "Moyenne: $moyenne"
else
        echo "Arguments non valide"
fi
```
