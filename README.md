# TP : Connexion à l'API Yelp avec Python

---

## Définitions (1/2)

`API` (Application Programming Interface) : Ensemble normalisé de méthodes permettant d'accéder à des fonctionnalités au services via un programme. En gros, c'est un moyen de faire communiquer deux applications.

`HTTP` (HyperText Transfer Protocol) : protocole de communication entre un client (celui qui demande) et un serveur (celui qui répond). Pour communiquer entre elles, les applications s'envoient des requêtes via ce protocole.

---

## Définitions (2/2)

`URL` (Uniform Resource Locator) : chaîne de caractères identifiant une ressource sur un réseau, et qui fournit les moyens d'agir sur cette ressource ou d'en obtenir une représentation, en décrivant son mode d'accès primaire ou « emplacement » réseau. Par exemple https://api.yelp.com/v3/businesses/search.

`JSON` (JavaScript Object Notation) : format de données textuelles permettant de représenter de l’information structurée

---

## Authentification

La plupart des API sont protégées pour éviter que n'importe qui puisse accéder aux données qu'elles envoient. La première étape lorsqu'on se connecte à une API est souvent de récupérer des accès.

Allez sur ce lien et suivez les instructions afin de récupérer un appId et un appSecret, et vérifier qu'ils fonctionnent :

- Etape 1 : Créez un compte sur Yelp (https://www.yelp.com/) 
- Etape 2 : Créez une application (https://www.yelp.com/developers/v3/manage_app)
- Etape 3 : Récupérez votre Client ID et votre API key

---

## Un premier appel (1/2)

- Etape 1 : Allez sur votre environnement Python (Spyder ou Jupyter)
- Etape 2 : Copiez-collez le code ci-dessous dans votre éditeur
- Etape 3 : Lancez le

```python
import requests 

base_url = "https://api.yelp.com/v3" 
url = base_url + "/businesses/search"
headers = {'Authorization': 'Bearer QmLeyvES(...)'} 
params = {"location": "Paris"} 
response = requests.get(url, headers=headers, params=params)
print(response.json())
```

---

## Un premier appel (2/2)

Vous allez récupérer un tableau JSON comportant une liste de 20 commerces situés à Paris.

---

## Décomposition du code (1/6)

Pour comprendre ce qu'il s'est passé, voici une explication pas à pas :

```python
import requests
```

Cette étape permet de dire à python quelles librairies on va utiliser. Ici, on a besoin du module requests pour appeler l'API Yelp et du module JSON pour lire la réponse que nous envoie cette API. Chaque librairie python a sa propre documentation (http://docs.python-requests.org/en/master/ pour requests).

---

## Décomposition du code (2/6)

```python
base_url = "https://api.yelp.com/v3" 
url = base_url + "/businesses/search"
```

Ici, on construit l'URL qui va nous permettre de chercher un commerce sur Yelp. Toutes les API ont une documentation décrivant les appels qu'on peut faire et les paramètres qu'on peut envoyer pour filtrer les résultats (https://www.yelp.com/developers/documentation/v3 pour celle de Yelp)

---

## Décomposition du code (3/6)

```python
headers = {'Authorization': 'Bearer QmLeyvES(...)'}
```

Afin de s'authentifier à l'API Yelp, il est nécessaire d'envoyer une clé en utilisant les headers de la requête. Un header permet d'envoyer des informations avec les requêtes concernant la communication qu'on souhaite établir. La plupart des API utilisent les headers pour gérer l'authentification. Toutes ces informations sont renseignées dans la documentation de l'API qu'on veut consommer (https://www.yelp.com/developers/documentation/v3/authentication pour celle de Yelp)

---

## Décomposition du code (4/6)

```python
params = {"location": "Paris"}
```

La plupart des ressources hébergées par une API peuvent être filtrées en utilisant des paramètres. La liste complète se trouve dans la documentation de la ressource qu'on essaie de récupérer via l'API (https://www.yelp.com/developers/documentation/v3/business_search pour chercher un commerce sur Yelp). Ici, nous avons renseigné le paramètre "location" à "Paris" pour récupérer des commerces à Paris.

---

## Décomposition du code (5/6)

```python
response = requests.get(url, headers=headers, params=params)
```

Cette partie du code utilise l'url, les headers et les paramètres que nous avons précédemment renseignés et envoie une requête HTTP avec le verbe "GET". Il existe plusieurs verbes HTTP pour décrire l'opération que nous souhaitons effectuer sur la ressource qu'on appelle (GET pour récupérer des données, POST pour créer des données, PUT ou PATCH pour mettre à jour des données, DELETE pour supprimer des données).

---

## Décomposition du code (6/6)

```python
print(response.json())
```

Cette opération sert à afficher le contenu JSON de la réponse. Dans le cas présent, il s'agit d'un tableau. On peut le parcourir en utilisant une boucle for pour, par exemple, stocker les données dans un fichier.

---

## Pour aller plus loin

Dans ce TP, nous nous sommes connectés à l'API Yelp, et avons récupéré des données. Pour continuer, vous pouvez tenter de récupérer des données via une autre ressources (par exemple, récupérer les reviews d'un business après avoir récupéré son ID yelp dans la réponse de la recherche en utilisant cette ressource : https://www.yelp.com/developers/documentation/v3/business_reviews), ou stocker ces données dans un fichier csv (https://docs.python.org/2/library/csv.html)