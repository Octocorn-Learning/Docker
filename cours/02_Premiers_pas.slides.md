---
title: Docker - Premiers pas
theme: solarized
author: Alexandre Devos
company: Octocorn
contributors: 
  - Alexandre Devos
sources:
  - 
---

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" -->

---

# Play with Docker


- Site permettant de manipuler des conteneurs Docker en ligne

- Permet de tester Docker sans rien installer

- [Play with Docker](https://labs.play-with-docker.com/)

> Vous devrez vous créer un compte DockerHub

----

## Play with Docker
#### Créer un conteneur


- Cliquez sur `+ ADD NEW INSTANCE`

- Lancez un conteneur `hello-world` avec la commande `docker run hello-world`

> Si vous souhaitez pratiquer les commandes sans installation !

----

## En local
#### Hello World


- Démarrez Docker Desktop

- Gardez un œil sur la liste des conteneurs

- Lancez un conteneur `hello-world` avec la commande `docker run hello-world`

> Que s'est-il passé ? Le conteneur est-il allumé ?

Note: Le conteneur s'est arrêté après avoir affiché le message. Il est donc terminé. Cf chapitre suivant

---

# Cycles de vie

![Docker Lifecycle](assets/docker-lifecycle.jpg) <!-- .element width="70%" -->

----

## Cycle de vie
#### Pull de l'image


- Le moteur vérifie la présence de l'image en local,

- Si l'image n'est pas présente, elle est **téléchargée** depuis le registre (DockerHub),

- On peut stocker ses images sur un registre privé (Github, Gitlab, Azure, AWS...)

- L'image est stockée en **local**.

> `docker pull <nom_image>`

----

## Cycle de vie
#### Création du conteneur


- À partir d'une image présente en local, le moteur crée un conteneur

- Des options peuvent être passées au conteneur (nom, réseau, volumes, ports...)

> `docker create <nom_image> [options]`

----

## Cycle de vie
#### Exécution du conteneur


- Le conteneur est lancé,

- Il exécute un processus spécifique situé dans l'image,

> `docker start <nom_conteneur>`

----

## Cycle de vie
#### La commande magique !


- Taper systématiquement `docker pull`, `docker create` puis `docker start` est fastidieux

- La commande `docker run` permet de créer et démarrer un conteneur en une seule commande !

> `docker run <nom_image> [options]`

----

## Cycle de vie
#### Arrêt du conteneur


- Le conteneur est arrêté,

- Il entre automatiquement dans l'état 'terminé' une fois le processus terminé.

- Le conteneur reste présent mais avec l'état 'terminé' et n'est plus en mémoire.

> `docker stop <nom_conteneur>`  
> `docker start <nom_conteneur>`

----

## Cycle de vie
#### Pause du conteneur


- Le conteneur est mis en pause,

- Il est toujours présent en mémoire,

- Il est toujours allumé,

- Il ne consomme plus de ressources.

> `docker pause <nom_conteneur>`  
> `docker unpause <nom_conteneur>`

----

## Cycle de vie
#### Suppression du conteneur


- Le conteneur est supprimé.

- Il n'est plus présent dans la liste des conteneurs.

- L'image reste présente en local.

> `docker rm <nom_conteneur>`

---

# Getting started

![Docker Lifecycle](assets/docker-lifecycle.jpg) <!-- .element width="70%" -->

----

## Getting started
#### First step !

`docker run -d -p 80:80 docker/getting-started`


- `-d` : Détaché, le conteneur s'exécute en arrière-plan

- `-p` : Publish, on publie le port 80 du conteneur sur le port 80 de la machine hôte

- `docker/getting-started` : Nom de l'image

> Docker créé un conteneur avec un nom par défaut

Note: Nous reviendrons sur les ports et les réseaux plus tard

----

## Getting started
#### Vérification

> Le conteneur est toujours allumé. Pourquoi ?

----

## Getting started
#### Vérification


- `docker ps` : Liste les conteneurs en cours d'exécution

- `docker ps -a` : Liste tous les conteneurs

- `docker logs <nom_conteneur>` : Affiche les logs du conteneur

> Il est possible de taper les 4 premiers caractères l'ID du conteneur au lieu de son nom.

----

## Getting started
#### Vérification

- Sur les logs, on peut voir qu'un serveur est lancé sur le port 80

- Le port est aussi précisé sur Docker Desktop

- Rendez-vous sur `http://localhost:80` pour voir le résultat

----

# Démonstration !

Note: ./Espace formateur/demos/01_Getting_started.md

----

## Getting started
#### Naviguer dans les fichiers

`docker exec -it <nom_conteneur> sh`

- `exec` : Exécute une commande dans le conteneur

- `-it` : Interactive, on se connecte au conteneur en mode interactif

- `<nom_conteneur>` : peut être remplacé par les 4 premiers caractères de l'ID

- `sh` : Shell, on lance un shell dans le conteneur

Note: `docker ps` pour récupérer l'id du conteneur

----

## Getting started
#### Naviguer dans les fichiers

Commandes de base linux :

- `ls -l` : Liste les fichiers

- `cd <nom_dossier>` : Se déplacer dans un dossier

- `cat <nom_fichier>` : Afficher le contenu d'un fichier

- `exit` : Quitter le shell

---

## Cheat sheet
#### Les commandes à retenir

- `docker run -d <nom_image>` : Créer et démarrer un conteneur

- `docker ps` : Liste les conteneurs en cours d'exécution

- `docker run -it <nom_image> sh` : Se connecter au conteneur en mode interactif shell

---

# La suite !

- [Index](index.html)