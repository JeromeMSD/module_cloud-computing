# Travaux dirigés

Vous allez réaliser une **Calculatrice Cloud** !

Le projet de CI/CD étant un [![](https://img.shields.io/badge/PROJET_TERMINÉ_🚀-059142?style=for-the-badge&logoColor=white)](https://dev.to/envoy_/150-badges-for-github-pnk) 

Vous avez maintenant toutes les clés pour la réalisation de ce premier petit projet !

## Propos

A partir des échanges que nous avons eu en cours concernant la calculatrice dans le cloud, réalisé la dite calculatrice !

ℹ️ Utilisez votre session codespace pour ce TD

### Avant la réalisation du TD

#### On n'oublie pas les bonnes habitudes

1. Créer un dépôt privé avec un nom commençant par `4A_[ ILC ou SQR ]_`
2. Ajoutez le second membre du binôme en tant que collaborateur.
3. Ajoutez-moi en collaborateur → jerome.massard@kiowy.com

#### Ni les bonnes pratiques

* `README.md` → pour votre vous du futur, il vous remerciera. 🚀
* `.gitignore` contenant `**/__pycache__` → pour ne pas embarquer le superflu.

## Etape de réalisation

### Comme un goût de CI/CD

![](https://img.shields.io/badge/python-059142?style=for-the-badge&logo=python&logoColor=white) ![](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)

Concevoir une API simple ( Python/Flask ou Rust ).
ℹ️ Vous pouvez reprendre le projet du module précédent en base.

La calculatrice doit permettre les **additions**, les **soustractions**, les **multiplications** et les **divisions**.

Pour demander ces calcules :
● `POST` &nbsp;: Envoyer un tuple pour demander un calcul ( renvoie un id ).
● `GET`  &emsp;: Récupérer le résultat via un id.

Pour l'instant, les résultats sont stockés dans une variable dictionnaire.

> Bonne pratique : pour plus de clareté utilisez un préfix pour vos routes api.
> **exemple :**`/api/ma_route` ou `/v1/ma_route` pour le versionning des endpoints.

Utilisez `curl` pour demander des calculs et récupérer le résultat.

```bash
# Rappel
curl -X POST/GET -h localhost:PORT -d "tuple={}"
```

### Externaliser la donnée

**L’API peut tomber 😱**

Et que se soit par contrainte produit ou *par goût de la chose bien faite* :
On ne va pas perdre toutes les demande de calcule pour un calcul impossible !

Utilisons [Redis](https://redis.io/docs/about/) comme service externe pour la gestion des résultats.

#### Redis

Utiliser Redis comme serveur de données, c’est un système de stockage **clé/valeur** qui utilise le port **6379** pour communiquer. Vous pouvez le lancer dans un conteneur via la commande suivante :

```bash
# À exécuter dans un autre terminal.
docker run -p 6379:6379 --name myredis redis
```

Oui, on pourrait utiliser `-d` pour lancer le conteneur en mode `detached` mais dans un terminal on peut voir les logs, pratique pour débuguer ! 🧐

Enfin utilisez [redis-cli](https://redis.io/docs/ui/cli/) pour accéder à redis et testez les commandes `set`, `get`, `keys`.

#### Mise en place dans l'API

Connectons maintenant l’API à la Redis
Documentation 👉 [python et redis](https://pypi.org/project/redis/)

```python 
import redis
r = redis.Redis(host='localhost', port=6379, db=0)

# Ajout de variable
r.set('foo', 'bar')                 # Retourne True si réussite

# Lecture de 
r.get('foo')                        # Retourne la value de foo
```

Remplacer le stockage précédemment en variable par un stockage via **Redis**

Utilisez `curl` pour demander des calculs et récupérer le résultat.

### Queue

![WIP](https://img.shields.io/badge/WIP-FA7343?style=for-the-badge&logoColor=white)

### Implémenter une interface utilisateur

#### Vous êtes déjà là ?! 🤯

Tout d’abord **Félicitation !** Vous avez fini le sujet principal.
Ça vous dit un peu de design et d’implémentation d’interface ?

**Une seul consigne :**
Créer un frontend qui permet à l’utilisateur de saisir et d’envoyer des demandes de calcul à l’API.

> Tips : vous pouvez utiliser le bon vieux combo **HTML/CSS/JS**
> &emsp; &emsp;&emsp;ou ChatGPT ( pour gagner du temps uniquement 😉)
