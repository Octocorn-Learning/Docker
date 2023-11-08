# Dockerfile : Exercice 1

L'objectif de cet exercice est de créer un conteneur Docker capable de servir une application simple.
L'application en question est une page web (html) qui affiche un chat donc le regard suit la souris.

## Précisions

- Nous n'avez pas besoin de modifier le code de l'application
- Vous pouvez utiliser l'image nginx que vous souhaitez

> Pensez à vien lire la documentation de l'image que vous utilisez !

## Dockerfile

Commencez par créer un fichier `Dockerfile` à la racine du projet.

La première instruction à écrire est l'image de base.

> Je vous invite à utiliser l'image `nginx:alpine`
> Vous trouverez la documentation de l'image [ici](https://hub.docker.com/_/nginx)
> L'instruction en question est `FROM`

Ensuite, il faudra copier les éléments du projet dans le conteneur.

> L'instruction en question est `COPY`
> Les applications Nginx sont stockées dans le dossier `/usr/share/nginx/html`
> N'oubliez pas que `.` représente le dossier courant

Enfin, il faudra exposer le port 80 du conteneur.

> L'instruction en question est `EXPOSE`

Créez également un fichier pour ignorer les fichiers et dossiers inutiles !

> .dockerignore, afin d'ignorer le Dockerfile ;)

## Construction de l'image

Une fois le Dockerfile écrit, vous pouvez construire l'image.

> L'instruction en question est `docker build`
> N'oubliez pas de nommer votre image avec l'option `-t`
> N'oubliez pas le point à la fin de la commande !

## Lancement du conteneur

Une fois l'image construite, vous pouvez lancer un conteneur à partir de cette image.

> L'instruction en question est `docker run`
> N'oubliez pas de nommer votre conteneur avec l'option `--name`
> N'oubliez pas de lier le port 80 du conteneur avec le port 80 de l'hôte avec l'option `-p`

## Vérification

Une fois le conteneur lancé, vous pouvez vérifier que l'application est bien accessible.
Si vous voyez le piti chat, c'est tout bon !