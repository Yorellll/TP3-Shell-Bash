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

echo "Les 2 paramètres concaténé donnent : $final"




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



listedir.sh ---> a faire

LISTE DES UTILISATEURS

Le problème est que cela nous donne, absolument tous le fichier et toutes les informations, nous souhaitons cependant tout trier.
Voici la solution avec cut : for user in $(cut  -d: -f1,3 /etc/passwd); do echo $user; done
Voici la solution avec awk : for user in $(awk -F: '$3 > 100 {print $1 $3}' /etc/passwd); do echo $user; done
