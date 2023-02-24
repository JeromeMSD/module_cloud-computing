# Projet noté

[🇺🇸 - 🇬🇧 English version](project.md)

||||
:--- | :---: | :---:
[![uB](img/UB.png)](https://u-bourgogne.fr/) | ESIREM - 4A - ILC/SQR <br/> Cloud computing <br/> **[ EXAMEN PRATIQUE ]** | [![ESIREM](img/ESIREM.png)](https://esirem.u-bourgogne.fr/)
|| Ce projet à rendre au plus tard le <br/> `7 avril 2023 à 23h59` ||

## Sommaire

* [Sujet](#exigences-pour-le-projet)
* [Exigences projet](#exigences-pour-le-projet)

---

Le projet noté du module de Cloud computing évaluera compétences et bonnes pratiques de développement vues en cours. La notation tiendra compte des fonctionnalités déployées dans l’API, de la bonne mise en place des points d’exigences projets ainsi que de la collaboration entre les membres du groupe.

---

## Sujet

Nous allons refaire
[![Twitter](https://logos-world.net/wp-content/uploads/2020/05/Twitter-Logo-2010.png)](https://twitter.com)

### Déroulé

#### Faire place net

Utiliser le dépôt de TD. ( vous pouvez le renommer si besoin )
Déplacez votre travail de TD ( fichiers, dossiers et README.md ) dans un dossier du même nom à la racine du dépôt.

Créez un nouveau README.md à la racine du projet qui servira de rapport pour le projet avec pour l’instant membres du groupe.

Vous viendrez l’agrémenter avec le déroulé du projet, les technologies utilisées, des badges, des badges de résultats de l'exécution des CIs et la procédure pour exécuter les composantes du projet.

Vous organiserez votre dépôt GitHub avec deux dossiers à la racine du projet à côté du README principal:

* un pour le `frontend` pour le code de l'interface utilisateur.
* un pour le `backend`, pour le code de votre API.

Chacun d’eux contenant un **README** spécifique et un **Dockerfile** permettant de lancer les programmes dans des conteneurs.

> Pas de `swagger.yaml` pour ce projet.

#### API

Concevoir une API simple ( `Python/Flask`, `Node` ou `Rust` ).

* Afficher tous les tweets.
* Enregistrer un tweet dans Redis.
* Attribuer un tweet à une personne.
* Retweeter.
* Afficher les sujets.
* Afficher les tweets liés à un sujet.

> **[ Tips ]** Avant de mettre en place les bases Redis, vous pouvez utiliser des dictionnaires pour tester vos routes et vos fonctionnalités.

Testez vos routes avec la commande `curl`.

[![WIP](https://img.shields.io/badge/WIP-FA7343?style=for-the-badge&logoColor=white)](https://www.youtube.com/watch?v=VBlFHuCzPgY)

##### Gestion des sujets

Tout simplement en créant une clé dédiée au sujet dans la table des utilisateurs.
⇒ Gérez les sujets comme des utilisateurs !

Vous pouvez utiliser des un préfix pour éviter les conflits de clé. Par exemple, les utilisateurs auront une clé au format u-username et les sujets h-hashtag. 

ℹ️ vous pouvez utilisez un autre format, précisez le dans le readme

> **[ Tips ]** Pour trier les liens entre sujets, utilisateurs et tweets tout se fera au traitement de la requête.

#### Redis

Pour externaliser le stockage et garantir leurs concervations en cas redémarrage de l'API, le tout dans une base rapide et sans contrainte vous utiliserez `redis`.

##### Qu'est ce que Redis

`Redis` est une base de donnée clé/valeur qui vous permettra de stocker de la donnée sous forme de dictionnaire.

Vous utiliserez Redis comme serveur de données, lancé dans un conteneur sur votre machine. Accessible une fois lancer via `localhost` sur le port `6379`.

Dans un autre terminal vous pouvez lancer `redis` frontalement via la commande :

```bash
docker run --name myredis -p 6379:6379 redis
```

> Tips : utilisez l'outil `redis-cli` pour accéder à `redis` directement sans script `python`.

Si vous stockiez vos tweets dans une variable dictionnaire vous pouvez maintenant la remplacer par un stockage dans le serveur `redis`.

##### Stocker les tweets via Redis

Vous stockerez les messages dans deux bases Redis.

Une base contenant les tweets.
*ex:* `key=timestamp, value=’{“author”: “username”, “tweet”: ”message”}’`
Une base contenant les utilisateurs dans laquelle la clé sera le nom d’utilisateur et en valeur la liste des clés de ses tweets.
*ex:* `key=username, value=[timestamp_1, timestamp_2, timestamp_3]`

L'architecture ci-dessus est un exemple. Vous êtes libre de choisir une autre architecture, mais elle doit fonctionner 😉

#### Tout est dans le détail 🧐

Il ne manque plus que l’interface utilisateur !

Avec la technologie de votre choix ( `HTML/CSS/JS`, `Node`, `VueJS`, `React`… ) réalisé un `frontend` pour communiquer avec votre API. Via boutons et formulaires, il permettra d’appeler les différentes routes de votre API et de mettre en forme les retours de l’API.

Laissez libre court à vos envies et votre imagination pour designer votre Twitter, la forme importe peu mais elle devrait **couvrir toutes fonctionnalités de l’API** décrite dans la section [API](#api) 🚀

ℹ️ N’oubliez pas le **Dockerfile** pour permettre le lancement du frontend dans un conteneur.
ℹ️ Vous décrivez les fonctionnalités du `frontend` dans le **README.md** de son dossier.

---

## Exigences pour le projet

Ce projet à rendre au plus tard le `7 avril 2023 à 23h59`.

> À partir de cette date, aucune modification du dépôt ou de code ne sera prise en compte.

### GitHub

Vous rendrez votre code via un dépôt GitHub, auquel vous m’aurez ajouté en tant que collaborateur.

* L’historique des changements sur le dépôt devra montrer la collaboration entre les membres du groupe ( changement de sources différentes sur les fichiers projet ).
* Une GitHub Action à chaque push pour vérifier `build` la syntaxe l'API à chaque `push` pour vérifier l'intgrité du code (*cf. projet CI/CD*).
* Le dépôt devra être documenté via 3 READMEs : un pour le `frontend`, un pour le `backend` et un global à la racine du dépôt.
* Le README principal contiendra les noms des **membres du groupe**, le **déroulé du projet**, les **technologies utilisées**, des **badges**, des badges de **résultats de l'exécution des CIs** et la **procédure** pour exécuter les composantes du projet.

> Vous n'avez pas à réaliser de `swagger.yaml` pour ce projet.

### Docker

* Un Dockerfile pour construire l'API (`backend`).
* Un Dockerfile pour construire le `frontend` si vous utilisez `Node`, `React` ou `VueJs`.

> **[ Tips ]** Si vous utilisez du `HTML/CSS/JS` utilisez un Dockerfile `nginx`.

### Redis

* Décrire la structure de donnée utilisée dans le **README backend**.
* Créez un script `python` pour charger dans la base de donnée `redis` des tweets et des utilisateurs par défaut. Ce script permettra d'avoir une base pour tester l'interface utilisateur.

### Interface utilisateur

* Détail des fonctionalités couvertes dans le **README frontend**.