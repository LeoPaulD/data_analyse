# data_analyse

# Installation de MyWebIntelligence sous Linux 

## Installer Docker

Référence du tutoriel : 

https://www.atlassian.com/fr/git/tutorials/install-git

Mettez à jour votre liste de packages existante 

´´´console
 sudo apt update 
 
 ´´´

Installer Git 

> sudo apt-get install git

Vérifier que git est installer et voir sa version

> git --version

Associer git à votre  nom et email github / bitbucket / gitlab ....

> git config --global user.name "Votre nom"

> git config --global user.email "votremail@mail.com"

## Installer Docker

Référence du tutoriel : 

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-fr

Mettez à jour votre liste de packages existante 

> sudo apt update

Installez quelques paquets pré-requis qui permettent à apt d'utiliser les paquets sur HTTPS 

> sudo apt install apt-transport-https ca-certificates curl software-properties-common

Ajoutez la clé GPG du dépôt officiel de Docker à votre système :

> curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Ajoutez le référentiel Docker aux sources APT :

> sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

Mettez à jour la base de données des paquets avec les paquets Docker à partir du référentiel qui vient d'être ajouté :

> sudo apt update

Installez Docker :

> sudo apt install docker-ce

Voir si Docker et installé et sa version : 

> docker --version

Le Docker devrait maintenant être installé, le démon démarré, et le processus autorisé à démarrer au boot. Vérifiez qu'il tourne :

> sudo systemctl status docker

## Préparer son espace de travail 

### MyWebIntelligencePython 

Référence du tutoriel :
https://github.com/MyWebIntelligence/MyWebIntelligencePython

Je souhaite cloner le projet dans mes documents, dans le dossier DNHD-DATA dans le terminal je tape :

> cd Documents/DNHD_DATA

Puis je clone le projet sur ma machine (disposer des fichiers sur ma propre machine)

> git clone https://github.com/MyWebIntelligence/MyWebIntelligencePython.git

Le fichier est maitenant sur mon ordinateur et je vais dans mon dossier MyWebIntelligencePython

> cd MyWebIntelligencePython/

Je construis mon image docker 

> sudo docker build -t mwi:1.0 .

je créais un chemin pour enregistrer mes données : 

Petite astuce, faire clic droit sur le dossier DNHD_DATA, paramètres pour connaitre le chemin jusqu'à ce dossier

> sudo docker run -dit --name mwi -v /home/leopaul/Documents/DNHD_DATA/data:/app/data mwi:1.0

### MyWebClient 

Référence du tutoriel :
https://github.com/MyWebIntelligence/MyWebClient


Je souhaite cloner le projet dans mes documents, dans le dossier DNHD-DATA dans le terminal je tape :

> cd Documents/DNHD_DATA

Puis je clone le projet sur ma machine (disposer des fichiers sur ma propre machine)

> git clone https://github.com/MyWebIntelligence/MyWebClient.git

Le fichier est maitenant sur mon ordinateur et je vais dans mon dossier MyWebClient

> cd MyWebClient/

Je construis mon image docker 

> sudo docker build -t mwiclient:1.0 .

je lance mon container pour que le voir dans mon navigateur :

Petite astuce, faire clic droit sur le dossier DNHD_DATA, paramètres pour connaitre le chemin jusqu'à ce dossier

> sudo docker run -p80:3000 --name mwiclient -v /home/leopaul/Documents/DNHD_DATA/data:/data mwiclient:1.0 











