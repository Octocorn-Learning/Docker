---
title: Docker - Docker Compose
author: Alexandre Devos
company: Octocorn
contributors: 
  - Alexandre Devos
sources:
  - 
---

# Docker Compose

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" -->

----

## Docker Compose
### Présentation

- Il est rare que tout le contenu d'une app (font, back, bdd, ...) soit dans un seul conteneur.
- Il est donc nécessaire de pouvoir lancer plusieurs conteneurs en même temps.

----

## Docker Compose
### Admettons...

Si je devais lancer une app web n tiers classique, je devrais : 
- Lancer un conteneur pour la base de données
- Lancer un conteneur pour le back
- Lancer un conteneur pour le front
- Créer les images de chacun de ces conteneurs
- Créer des volumes de persistence
- Créer un network et le lier à tous les conteneurs
- Et tout refaire à chaque mise à jour !

----

## Docker Compose
### Un fichier pour les gouverner tous

- Docker Compose permet de faire tout ça en une seule commande !
- Ce fichier est nommé `docker-compose.yml`, écrit en [YAML](https://fr.wikipedia.org/wiki/YAML).
- Il peut être partagé, inséré dans un dépôt git, etc.

---

# YAML

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" -->

----

## YAML
### Présentation

- **Y**et **A**nother **M**arkup **L**anguage
- Format .yaml ou .yml
- Format de données textuelles, comparable au JSON
- Utilisé pour la configuration de nombreux outils (Ansible, Docker, Kubernetes, etc.)

----

## YAML
### Présentation

- Il s'agit d'un langage de **sérialisation**
- Il sert à stocker des données brutes de manière structurée
- Fonctionne avec des **clés** et des **valeurs**
- Utilise l'indentation pour structurer les données

----

## YAML
### Exemple

```yaml
formation:
    titre: Docker
    duree: 2 jours
    niveau: débutant
author: 
    nom: Alexandre Devos
    societe: Octocorn
    stack:
      - Ecosystème Java
      - Ecosystème Javascript
      - DevOps
```

----

## YAML
### Equivalent JSON

```json
{
  "formation": {
    "titre": "Docker",
    "duree": "2 jours",
    "niveau": "débutant"
  },
  "author": {
    "nom": "Alexandre Devos",
    "societe": "Octocorn",
    "stack": [
      "Ecosystème Java",
      "Ecosystème Javascript",
      "DevOps"
    ]
  }
}
```

----

## YAML
### Types de données

- Les types d'objets primaires (int, str, float, bool etc.)
- Beaucoup de types de données (tableaux, listes ...)
- Pris en charge par le JavaScript, Python, Ruby, Java ...

> Il n'est pas destiné à remplacer le JSON, chacun ayant ses avantages.

----

## YAML
### Tips

> Si votre conteneur ne build pas : vérifiez votre indentation !

---

# Docker Compose

![Docker logo](assets/docker-logo.png) <!-- .element width="70%" -->

----

## Docker Compose
### Fonctionnement

- L'utilisateur écrit un fichier `docker-compose.yml`
- Il tape la commande `docker-compose up`
- Docker compose va :
  - Lire le fichier `docker-compose.yml`
  - Créer les conteneurs
  - Créer les volumes
  - Créer le network
  - Lancer les conteneurs
- L'utilisateur peut accéder à l'application

----

## Docker Compose
### Attributs

- Si on peut mettre 'ce que l'on veut' dans un fichier YAML, il faut tout de même respecter une structure.
- Concernant Docker Compose, il y a des attributs obligatoires et d'autres facultatifs.
- Il existe **beaucoup** d'attributs, nous n'en verrons que quelques uns.

> Liste complète [ici](https://github.com/compose-spec/compose-spec/blob/master/spec.md)

----

## Docker Compose
### Structure basique

```yaml
## Version de docker-compose
version: "3.9"

services: ## Obligatoire : liste des services.
  permierService: ## Nom du service (conteneur)
    ## Obligatoire : image de base. Equivbalent du FROM
    image: nginx:latest
    ports: ## Ports à exposer, comme pour le -p de docker run
      - 8080:80
    volumes: ## Volumes à monter. Même fonctionnement que docker run -v
      - ./nginx.conf:/etc/nginx/nginx.conf
  secondService:
    ## ...
  troisiemeService:
    ## ...
```

> Attention à l'indentation !

----

## Docker Compose
### `version`

- Indique la version de docker-compose utilisée
- La version 3.9 correspond à la version 19.03+ du moteur Docker

> Voir la [doc](https://docs.docker.com/compose/compose-file/compose-versioning/)

----

## Docker Compose
### `services`

```yaml
services:
  monservice:
```

- Liste des services (conteneurs) à créer
- Obligatoire
- Chaque service est un objet, avec ses propres attributs

----

## Docker Compose
### `monservice`

```yaml
services:
  monservice:
    attribut:
    attribut:
```

- Il y a une indentation entre le nom du service et ses attributs
- Le nom du service est libre, mais il est conseillé de le nommer comme le conteneur qu'il va créer

----

## Docker Compose
### `monservice.image`

```yaml
services:
  monservice:
    image: nginx:latest
```

- Indique l'image de base du conteneur
- Equivalent du `FROM` d'un Dockerfile

----

## Docker Compose
### `monservice.ports`

```yaml
services:
  monservice:
    ports:
      - 8080:80
```

- Indique les ports à exposer
- Equivalent du `-p` de `docker run`
- Le premier port est celui de l'hôte, le second celui du conteneur

----

## Docker Compose
### `monservice.volumes` : bind mount

```yaml
services:
  monservice:
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
```

- Indique les volumes à monter
- Equivalent du `-v` de `docker run`
- Le premier chemin est celui de l'hôte, le second celui du conteneur

----

## Docker Compose
### `monservice.volumes` : Volume Docker

```yaml
services:
  monservice:
    volumes:
      - nomVolume:/etc/nginx/nginx.conf
volumes:
  nomVolume:
```

- Permets ici de monter un volume Docker
- Equivalent du `-v` de `docker run`
- Le volume doit être déclaré dans la section `volumes`

----

## Docker Compose
### `monservice.depends_on`

```yaml
services:
  monservice:
    depends_on:
      - serviceA
      - serviceB
```

- Indique les dépendances entre les services
- Le service démarrera après les services dont il dépend

----

## Docker Compose
### `monservice.environment`

```yaml
services:
  monservice:
    environment:
      - PORT=8080
```

- Indique les variables d'environnement à passer au conteneur
- Equivalent du `-e` de `docker run`

> NB : beaucoup de conteneurs ont besoin de variable d'environnement !

----

## Docker Compose
### Commandes

- `docker-compose up` : lance les conteneurs du contexte courant
- `docker-compose up -d` : lance les conteneurs en mode détaché
- `docker-compose down` : arrête et supprime les conteneurs du contexte courant

----

## Docker Compose
### Démonstration

Docker run VS docker compose

----

## Docker Compose
### A vous de jouer !

Réalisez l'exercice 2.

----

## Docker Compose
### `monservice.build`

```yaml
services:
  monservice:
    build: ./chemin/vers/Dockerfile
```

- Indique le chemin vers le Dockerfile à utiliser
- Equivalent du `docker build` d'un Dockerfile
- Le fichier doit être présent dans le contexte courant

----

## Docker Compose
### `monservice.contexte`

```yaml
services:
  monservice:
    context: ./chemin/vers/contexte
```

- Indique le chemin vers le contexte à utiliser
- Permet de spécifier un contexte différent du répertoire courant
- Equivalent du `docker build -f ./chemin/vers/Dockerfile` d'un Dockerfile

----

## Docker Compose
### `monservice.dockerfile`

```yaml
services:
  monservice:
    dockerfile: Dockerfile.dev
```

- Indique le nom du Dockerfile à utiliser
- Permet de spécifier un Dockerfile différent de `Dockerfile`
- Utile quand on a plusieurs dockerfile dans le même contexte

----

## Docker Compose
### Rebuild

- Docker conserve en cache les images buildées
- Cela permet de ne pas avoir à tout refaire à chaque fois : il ne build que les couches modifiées
- Concernant les docker-compose, il faut utiliser l'option `--build` pour lui indiquer explicitement de rebuild les images

```shell
docker-compose up --build
```

----

## Docker Compose
### A vous de jouer !

Rendez vous sur ce [repository](https://github.com/Octocorn-Learning/docker-exercice3).
Vous y trouverez les énoncés de l'exercice !

---

# Fin

- Il reste encore beaucoup de choses à voir sur Docker, mais vous avez les bases !
- Certains éléments ont en effet été volontairement omis pour ne pas vous noyer.
- Si vous souhaitez m'aider à améliorer ce cours, n'hésitez pas à me contacter ou à consulter la charte de [contribution](https://github.com/Octocorn-Learning/Docker/blob/main/CONTRIBUTING.md)

----

## More ?

- Si vous que j'anime ce cours dans votre entreprise, n'hésitez pas à me contacter :
  - [LinkedIn](https://www.linkedin.com/in/alexandre-devos-720637168/)
  - [Mail](mailto:contact@octocorn.fr)
