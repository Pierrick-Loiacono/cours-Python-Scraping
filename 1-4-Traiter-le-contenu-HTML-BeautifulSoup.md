# Traiter le contenu HTML

### 1. Vue d'ensemble

**Beautiful Soup** est une bibliothèque Python permettant d’analyser et de parcourir le code HTML d’une page web. Elle transforme le HTML en une structure exploitable (arbre DOM), ce qui facilite la recherche et l’extraction d’éléments spécifiques comme des titres, des liens ou des tableaux.

Utilisée  avec ``Requests``, elle constitue un outil essentiel pour le web scraping, en permettant de cibler précisément les données souhaitées à l’aide de méthodes simples (find, find_all) ou de sélecteurs CSS.

En résumé, Beautiful Soup permet :

- d'analyser de l'HTML
- naviguer dans la structure d'une page
- extraire des données ciblés

--- 

### 2. Installation

```bash
pip install beautifulsoup4
```

### 3. Premier exemple

```python
from bs4 import BeautifulSoup

html = """
<html>
    <head>
        <title>Titre de la page</title>
    </head>
    <body>
        <h1>Un titre principal</h1>
        <p>Paragraphe</p>
    </body>
</html>
"""

soup = BeautifulSoup(html, "html.parser")
print(soup.title.text) # Affichera "Titre de la page"
```

### 4. Méthodes principales

#### **``find()``** : un seul élément

``find`` permet de récupérer un seulement en fonction de sa balise ou de l'identifiant de celle-ci

```python
titre = soup.find("h1")
print(titre.text)
```

> ! ATTENTION : Si vous faites un **`find`** sur un élément qui n'est pas présent, alors python retournera None, ce qui fera planter le programme si vous tenter d'afficher le texte de celui-ci
#### **``find_all()``** : plusieurs éléments

``find`` permet de récupérer un seulement en fonction de sa balise ou de l'identifiant de celle-ci

```python
paragraphes = soup.find_all("p")

for p in paragraphes:
    print(p.text)
```

#### Filtrer avec des attributs

`class` étant un mot réservé en pyton pour définir une classe d'objet, il faudra utiliser `class_` pour cibler l'attribut HTML `class`

Ici on utilise `find` donc on recupere qu'un seul élément, mais on peut très bien utiliser ``find_all()``

```python
soup.find("div", class_="article")
```

#### Filtrer avec sélecteur CSS

Ici plutot que de cibler l'attribut de classe HTML, on cible directement un sélecteur CSS, qui nous retourne forcément une liste de ce qu'il a trouvé et non un seul élément.

```python
soup.select(".article")
```
---


### 5. Exemple complet

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)
if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")

    articles = soup.find_all("article")

    if articles : 
        for article in articles:
            print(article.text.strip())
    else:
        print("Aucun résultat, trop dommage")
else:
    print("Erreur")

```