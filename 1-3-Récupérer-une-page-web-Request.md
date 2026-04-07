# Récupérer une page Web

### 1. Vue d'ensemble

La bibliothèque **Request** perment d'envoyer des requêtes HTTP depuis Python. Elle simule le comportement d'un navigateur en récupérant le contenu HTML renvoyer par un serveur. Le traitement de ces données sera vu dans le prochain chapitre.

Elle permet donc :
- d'accéder à une page web
- envoyer des données
- récupérer une réponse

--- 

### 2. Installation et première utilisation

**Installation**

```bash
pip install requests
```

**Exemple d'utilisation**

```python
import requests

url = "https://example.com"
response = requests.get(url)

print(response.status_code)
print(response.text)
```
### La réponse (response)

L'objet **response** contient toutes les informations que le serveur à renvoyé au "navigateur"

#### Code de statut

C'est le retour indiquant si la requête a fonctionnée ou si une erreur a été rencontrée. Il y a 4 familles de code retour 
- 2xx : Ok
- 3xx : Redirection (peut être concidéré comme Ok)
- 4xx : Erreur côté client. **404** quand un contenu n'est pas trouvé
- 5xx : Erreur côté serveur.

#### Contenu HTML

Le contenu HTML c'est l'intégralité de la page récupérée. Pour rappel le **HTML** (HyperText Markup Language) c'est un langage de balisage qui définit la structure d'une page web.
```html
<!DOCTYPE html>
<html lang="fr">
    <head>
        <title>Titre de ma page</title>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="style.css"/>
    </head>
    <body>
...
```

On récupére toute la page grace à la ligne suivante :

```python
response.text
```


### 3. Conditionner

Vous connaissez les conditions en programmation, une chose simple a faire de vérifier le code retour pour éviter de délencher des erreurs inutilement.


```python
if response.status_code == 200:
    # Le traitement si c'est tout bon 
else:
    # Affiche une erreur ou log l'erreur
```
### 4. Modifier le User-Agent

Le User-Agent c'est un header HTTP envoyé avec chaque requête. Il indique au serveur quel type de client fait la requête


Exemple : ``Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36``

Le problème c'est que quand on utilise simplement la bibliothèque **``Request``** le User-Agent a cette tête : ``python-requests/2.x.x`` et certains sites peuvent le bloquer

La solution est toute simple même si elle ne règle pas tout, on peut simuler un autre User-Agent pour éviter le blocage :

```python
import requests

url = "https://example.com"

headers = {
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(url, headers=headers)

```

Les serveurs peuvent détecter les bots ou les scripts automatisés, c'est pour ça qu'ils peuvent :
- bloquer la requête
- renvoyer une page vide
- renvoyer un contenu différent
- afficher un captcha

#### Les limites

Ça suffit pas toujours, certains sites mettent en place des règles très stricts tel que :

- vérification de l'adresse IP
- la fréquence des requêtes
- le JavasScript
- le comportement utilisateur

Pour faire du scrapping avancé, il vous faudra des outils bien plus spécifique

### 5. Copier un contenu

Pour éviter de faire trop de requête sur un serveur inutilement, vous pouvez simplement copier son contenu. Pour ça, faites la requête sur l'URL et enregistrer le contenu dan sun fichier

```python
html = requests.get(url).text

with open("page.html", "w") as f:
    f.write(html)
```
La variable ``contenu`` aura la même tête que ``response.text``

### 6. Scrap un fichier en local

Avec **Request** vous ne pouvez scrapper que des sites (accessible via une URL). Si vous voulez scrapper un fichier en local pour faire des tests ou autre, vous pouvez récupérer le contenu de votre fichier HTML en ouvrant le fichier avec Python.

```python
with open("articles.html", "r", encoding="utf-8") as f:
    contenu = f.read()
```
La variable ``contenu`` aura la même tête que ``response.text``






---


