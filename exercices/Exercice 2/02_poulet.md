# Docker Compose : MongoDB

Votre objectif est de monter une stack applicative avec MongoDB et MongoExpress.

## Consignes

> Pensez à lire la documentation

### MongoDB

- Vous devez utiliser la dernière image officielle de MongoDB
- Vous utiliserez un volume docker nommé `mongo_data` pour la persistance des données
- Vous n'exposerez aucun port

> Utilisez bien un volume docker et non un bind mount

### MongoExpress

- Vous utiliserez l'image officielle, dernière version
- Le port coté host doit être 8090
- Ce service doit toujours démarrer après MongoDB

> Le port hôte est toujours à gauche, le port conteneur à droite