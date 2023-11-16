⚠️CE PROJET A ÉTÉ RÉALISÉ DANS UN CADRE UNIVERSITAIRE. IL A ÉTÉ DÉPOSÉ SUR CE GIT POUR CORRECTION, LE CODE PEUT DONC CONTENIR DES ERREURS⚠️

# TP3-Shell-Bash

                                     analyse.sh                                                
#!/bin/bash

paramNumber=$#

scriptName=$0

thirdParam=""

if [ $paramNumber -ge 3 ]; then
    thirdParam=$3
fi

echo "Bonjour, vous avez rentré $paramNumber paramètres."
echo "Le nom du script est : $scriptName"
echo "Le 3ème paramètre est $thirdParam"
echo "Voici la liste des paramètres"

for i in "$@"; do
    echo "$i"
done


                                      concat.sh   

#!/bin/bash

paramNumber=$#

if [ $paramNumber -ne 2 ]; then
    echo "Vous devez mettre 2 paramètres"
    exit
fi

final=$1$2

echo "Les 2 paramètres concaténés donnent : $final"




							fileTest.sh
                            
#!/bin/bash
     
paramNumber=$#

if [ $paramNumber -ne 1 ]; then
    echo "Il y a trop de paramètres"
    exit
fi

file=$1
type=""
lecture=""
ecriture=""
executable=""
user=$(ls -l $file | cut -d' ' -f3)

if [ -e $file ]; then
    echo "Le fichier existe"
else
    echo "Le fichier n'existe pas"
    exit
fi

if [ -f $file ]; then
    echo "C'est un fichier lambda"
    type="fichier ordinaire"
elif [ -d $file ]; then
    echo "C'est un dossier"
    type="répertoire"
fi


if [ -r $file ]; then
    echo "Vous avez le droit de lecture"
    lecture="est accessible en lectre"
else
    echo "Vous n'avez pas le droit de lecture"
fi

if [ -x $file ]; then
    echo "Vous avez le droit d'execution"
    executable="possède les droits d'éxécutions"
else
    echo "Vous n'avez pas le droit d'execution"
fi

if [ -w $file ]; then
    echo "Vous avez le droit d'éxecution"
    ecriture="droit d'écriture"
else
    echo "Vous n'avez pas le droit d'éxécution"
fi

echo "Le fichier $file est un $type, qui $lecture $executable $ecriture, accessible par $user"



						listedir.sh

#!/bin/bash

if [ $# -ne 1 ]; then
    echo "Usage: $0"
    exit 1
fi

folder="$1"

echo "Sub folder in $folder :"
for sous_repertoire in "$folder"/*; do
    if [ -d "$subFolder" ]; then
        echo "    $subFolder"
    fi
done


						LISTE DES UTILISATEURS

Le problème est que cela nous donne, absolument tous le fichier et toutes les informations, nous souhaitons cependant tout trier. </br>
Voici la solution avec cut : "for user in $(cut  -d: -f1,3 /etc/passwd); do echo $user; done" </br>
Voici la solution avec awk : "for user in $(awk -F: '$3 > 100 {print $1 $3}' /etc/passwd); do echo $user; done"


						doesExist.sh
#!/bin/bash

if [ $# -ne 1 ]; then
    echo "Usage: $0"
    exit 1
fi

input="$1"

if [[ "$input" =~ ^[0-9]+$ ]]; then
    userUid="$input"
else
    userUid=$(id -u "$input" 2>/dev/null)
fi

if [ -n "$userUid" ]; then
    echo "L'UID de l'utilisateur $input est : $userUid"
fi

						createUser.sh


#!/bin/bash

if [ "$(id -u)" -ne 0 ]; then
    echo "You have to be a root user"
    exit 1
fi

checkUseExistence() {
    local username="$1"
    id "$username" &>/dev/null
}

read -p "Login: " login

if check_user_existence "$login"; then
    echo "$login existe déjà."
    exit 1
fi

read -p "Nom : " nom
read -p "Prénom : " prenom
read -p "UID : " uid
read -p "GID : " gid
read -p "Commentaires : " commentaire

homeDir="/home/$login"
if [ -d "$homeDir" ]; then
    echo "$homeDir existe déjà."
    exit 1
fi

useradd -c "$commentaire" -d "$homeDir" -u "$uid" -g "$gid" "$login"

echo "Le compte utilisateur $login a été créé avec succès dans $homeDir."


						note.sh

#!/bin/bash

while true; do
    read -p "Saisissez une note (ou 'q' pour quitter) : " note

    if [ "$note" == "q" ]; then
        echo "Au revoir !"
        exit 0
    fi

    if ((note >= 16 && note <= 20)); then
        echo "Très bien"
    elif ((note >= 14 && note < 16)); then
        echo "Bien"
    elif ((note >= 12 && note < 14)); then
        echo "Assez bien"
    elif ((note >= 10 && note < 12)); then
        echo "Moyen"
    elif ((note < 10)); then
        echo "Insuffisant"
    else
        echo "Note non valide. Veuillez saisir une note entre 0 et 20."
    fi
done


						
