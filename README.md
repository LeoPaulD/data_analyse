# Installation de MyWebIntelligence sous Linux 

## Installer GIT

Référence du tutoriel : 

https://www.atlassian.com/fr/git/tutorials/install-git


Mettez à jour votre liste de packages existante 

> sudo apt update 



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

Si votre port 80 est déjà encombrer par skype ou votre serveur local apache pensez à changer le port d'écoute par le port 8080 par exemple 

> sudo docker run -p80:3000 --name mwiclient -v /home/leopaul/Documents/DNHD_DATA/data:/data mwiclient:1.0 


# Installer et utiliser Google BookMarklets 

## Installation

Informations sur l'outil.

https://medialab.sciencespo.fr/outils/google-bookmarklets/


Récupérer l'outil en le faison glisser dans sa barre de favoris.

https://medialab.github.io/google-bookmarklets/


## Utilisation 

* Faire une recherche sur google 

* Lancer ExtractGoogle depuis ses favoris

* Récuprer les urls de sa recherche google. 

* Télécharger le CSV de tous les urls collecté

* Nettoyer ce fichier pour le rendre compatilble avec MyWebIntilligence 

* Pendant le nettoyage, on ne récupère que la colonne url

* On met toutes nos urls dans un fichier txt

### Les bonnes pratiques :


* Cibler sa recherche sur des dates précises, plus les extractions sont précises, mieux sont les résultats

* Utiliser google trends pour trouver les péridodes les plus intéressante à chercher.



# Utilisation de MyWebIntelligencePython

Ouvrir le terminal de son conteneur docker qui porte comme nom mwi :

> docker exec -it mwi bash

## Créer un nouveau projet :

Créer un nouveau projet, une nouvelle land

> python mywi.py land create --name=LAND_NAME --desc=LAND_DESCRIPTION

exemple :
> python mywi.py land create --name=Branco --desc="Projet d'analyse de controverse sur Juan Branco et son livre crépuscule"

Voir la liste des lands dans ce projet mwi

> python mywi.py land list

Créer un dictionnaire 

> python mywi.py land addterm --land=LAND_NAME --terms=TERMS

exemple 

> python mywi.py land addterm --land=Branco --terms="Branco, crépuscule"

Créer un liste d'urls 

Manuellement 

> python mywi.py land addurl --land=LAND_NAME --urls=URLS  

exemple 

> python mywi.py land addurl --land=Branco --urls="https://www.marianne.net/culture/crepuscule-juan-branco-livre-critique, https://www.franceculture.fr/emissions/signes-des-temps/de-quoi-crepuscule-de-juan-branco-est-il-le-signe"

Avec un fichier txt 

> python mywi.py land addurl --land=LAND_NAME --path=PATH

exemple 

> python mywi.py land addurl --land=Branco --path=data/Url_Branco.txt

 Lancer le crowl 

 > python mywi.py land crawl --name=LAND_NAME --limit=LIMIT

 exemple 

 > python mywi.py land crawl --name=Branco --limit=25


Crowler le domaine :

> python mywi.py domain crawl [--limit=LIMIT, --http=HTTP_STATUS]

Exporter les lands :

les différents type :

> type = ['pagecsv', 'pagegexf', 'fullpagecsv', 'nodecsv', 'nodegexf', 'mediacsv']

> python mywi.py land export --name=LAND_NAME --type=EXPORT_TYPE --minrel=MINIMUM_RELEVANCE

exemple 

Premier export minrel=0 pour avoir l'entierté des liens 

Mais pour l'exploitation on peut commmencer à 3

> python mywi.py land export --name=Branco --type=pagecsv --minrel=0











