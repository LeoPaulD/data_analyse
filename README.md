# data_analyse

# Installation de MyWebIntelligencesous Linux 

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

Je souhaite cloner le projet dans mes documents, dans le dossier DNHD-DATA dans le terminal je tape :

> cd Documents/DNHD-DATA

Puis je clone le projet sur ma machine (disposer des fichiers sur ma propre machine)

> git clone https://github.com/MyWebIntelligence/MyWebIntelligencePython.git

Le fichier est maitenant sur mon ordinateur et je vais dans mon dossier MyWebIntelligencePython

> cd MyWebIntelligencePython/

Je construis mon image docker 

> sudo docker build -t mwi:1.0 .

je créais un chemin pour enregistrer mes données : 

> sudo docker run -dit --name mwi -v /Documents/DNHD-DATA/data:/app/data mwi:1.0

### MyWebClient 

Je souhaite cloner le projet dans mes documents, dans le dossier DNHD-DATA dans le terminal je tape :

> cd Documents/DNHD-DATA

Puis je clone le projet sur ma machine (disposer des fichiers sur ma propre machine)

> git clone https://github.com/MyWebIntelligence/MyWebClient.git

Le fichier est maitenant sur mon ordinateur et je vais dans mon dossier MyWebClient

> cd MyWebClient/

Je construis mon image docker 

> sudo docker build -t mwiclient:1.0 .

> docker run -p80:3000 --name mwiclient -v /Documents/DNHD-DATA/data:/app/data mwiclient:1.0












