---
title: Docker - DockerFile
author: Alexandre Devos
company: Octocorn
contributors: 
  - Alexandre Devos
sources:
  - 
---

# Custom Images
### Docker commit

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" align="left" -->

----

## Custom images
### Introduction

- La création d'image via ligne de commande est **fastidieuse**.
- Les conteneurs étant locaux, ils sont **difficiles à partager**.
- Deux méthodes pour créer une image : 
  - Via **ligne de commande** et envoi sur un **registre**
  - Via **Dockerfile**

----

## Custom Images
### Ligne de commandes

- Création d'un conteneur
- Modification du conteneur
- Création d'une image à partir du conteneur
- Partage de l'image sur un **registre**

> Cette méthode est relativement peu utilisée !

----

## Custom Images
### Docker commit

- La commande docker commit permet de créer une image à partir d'un conteneur

Syntaxe :

```shell
docker commit [OPTIONS] CONTAINER <REPOSITORY<:TAG>>
```

----

## Custom Images
### Démonstration

Création d'une image ubuntu custom

Note: ./demo/04_commit.md

----

## En conclusion

- Bien que ça puisse être pratique, ça reste **fastidieux**.
- Il est possible d'automatiser tout ça avec un **Dockerfile** !

---

# Custom Images
### Dockerfile

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" align="left" -->

----

## Dockerfile
### Définition

- Un Dockerfile est un **script** qui permet de construire des images.
- Il est constitué d'une suite d'instructions, suivant une syntaxe définie.

> [RTFM](https://docs.docker.com/engine/reference/builder/)

----

## Dockerfile
### Instructions courantes

```dockerfile
FROM # Définit l image de base (parent)
LABEL # Ajoute des métadatas
ARG # Variables utilisables uniquement par le dockerile
ENV # Variables utilisables par le dockerfile ET les conteneurs créés
RUN # Exécute une commande lors de la création de l image
COPY # Permet de copier des fichiers
ADD # Idem COPY, mais permet de décompresser les archives
ENTRYPOINT # définit la commande de démarrage du conteneur
CMD # Spécifie les arguments envoyés aux ENTRYPOINT sous forme de tableau ["cmd1", "cmd2"]
WORKDIR # Définit le répertoire de travail utilisé au lancement par CMD et ENTRYPOINT
EXPOSE # Définit le port exposé
VOLUME # Définit le volume du conteneur
USER # Désigne l utilisateur par défaut (root si non spécifié)
```

----

## Dockerfile
### Le contexte docker

- Le contexte docker est le répertoire dans lequel se trouve le Dockerfile.
- Lors de la création de l'image, le contexte est envoyé au démon docker.
- Le contexte est envoyé **en clair** au démon docker.
- Il est donc **déconseillé** d'y mettre des fichiers sensibles.

----

## Dockerfile
### .dockerignore

- Permet de lister des fichiers à exclure du contexte.
- Fonctionne comme un `.gitignore`.

----

## Dockerfile
### Commandes

`docker build` : Construit une image à partir d'un Dockerfile

```shell
docker build [OPTIONS] PATH | URL | -
```

> Pour désigner le répertoire courant, on utilise `.`

----

## Dockerfile
### Exemple

```shell
docker build -t myimage:latest .
```

- `-t` : Tag l'image avec le nom `myimage` et le tag `latest`
- `.` : Répertoire courant

> Attention à ne pas oublier le point !


----

## Dockerfile
### Travail dirigé

Montons ensemble un Dockerfile pour une application nodejs (express).

Note: ./Espace formateur/demos/05_DockerFile.md

----

## Dockerfile
### A vous de jouer !

Réalisez l'exercice 1

---

# Dockerfile
## Multi-stage

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" align="left" -->

----

## Dockerfile
### Multi-stage

- Permet de créer une image à partir d'une autre image.
- Permet de **réduire la taille** de l'image finale.

----

## Dockerfile
### Objectif

- La plupart des applications nécessitent des dépendances pour être compilées.
- Ces dernières servent uniquement à la compilation et ne sont pas nécessaires à l'exécution.
- Il est donc inutile de les inclure dans l'image finale.

----

## Dockerfile
### Exemple

```dockerfile
## Déclaration de la première étape
FROM ubuntu:latest as first_stage
RUN echo "Hello world" > /hello.txt

FROM alpine:latest
COPY --from=first_stage /hello.txt /hello.txt
```

----

## Dockerfile
### Explications

- On crée un fichier `hello.txt` dans un conteneur ubuntu.
- On crée étape qui va copier le fichier `hello.txt` dans un conteneur alpine.
- On utilise l'option `--from` pour spécifier l'étape à utiliser.
- On peut utiliser autant d'étapes que nécessaire.
- L'image finale sera la dernière étape.

----

## Dockerfile
### Travail dirigé

Montons ensemble un Dockerfile en multistage pour une application React.

---

# La suite !

[Docker Compose](06_Docker-Compose.slides.md)