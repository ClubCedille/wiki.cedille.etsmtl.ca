# wiki.cedille.etsmtl.ca
Documentation officielle du club CEDILLE avec le theme hugo [Docsy](https://www.docsy.dev/)

## 2024 Update

**Ce dépôt a été archivé. Le wiki du club cedille a été migré dans le dépôt [Plateforme Cedille](https://github.com/ClubCedille/Plateforme-Cedille) et disponible depuis [wiki.omni.cedille.club](https://wiki.omni.cedille.club/fr/)**



## Pour commencer

Configuration requise :

* [Hugo](https://gohugo.io/) (`apt install hugo`)

Alternativement :

* [Docker](https://docs.docker.com/get-docker/)
* [Docker-Compose](https://docs.docker.com/compose/install/)

# Usage

## Exécuter le site web localement
Une fois que vous avez fait votre copie de travail du repo du site, à partir du dossier racine du repo, exécutez :
```
npm install
hugo server
```

## Exécuter un conteneur localement
- Construisez et exécutez l'image docker construite
```
docker-compose up --build -d
```
Ouvrez votre navigateur web et tapez http://localhost:1313 dans votre barre de navigation, cela ouvre une instance locale de la page d'accueil de l'exemple docsy. Vous pouvez maintenant apporter des modifications à l'exemple docsy et ces modifications apparaîtront immédiatement dans votre navigateur après avoir sauvegardé.

### Nettoyage
Pour supprimer les images produites, exécutez
```
docker-compose rm
```
