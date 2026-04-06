# Les templates avec Jinja2

### 1. Stylisé nos pages


```mermaid
flowchart LR
    A[Template HTML] --> B[Lien vers CSS]
    B --> C[Fichier CSS dans /static]
    C --> D[Navigateur charge le style]
    D --> E[Page stylisée]
```

### Dossier static

**Exemple d'arborescence**

mon_projet/
│
├── ``app.py``
├── ``templates/``
│   └── ``base.html``
└── ``static/``
    └── ``css/``
        └── ``style.css``

### Lier le CSS dans un template

```html
<head>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
</head>
```

`` {{ url_for(...)}}`` va permettre de lié le CSS au template. Ce n'est pas la seule utilisation de cette fonction, on peut très bien faire de la redirection vers une autre URL (route)

Exemple : ``{{ url_for('index')}}``
### 2. Exemple complet

#### `base.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{% endblock %}</title>

    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
</head>
<body>

<header>
    <h1>Le site du futur</h1>
</header>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
```

#### `index.html`

```html
{% extends "base.html" %}

{% block title %}Accueil{% endblock %}

{% block content %}
<h1>Bienvenue</h1>
<p>Page stylisée avec CSS</p>
{% endblock %}
```

#### `static/css/style.css`

```css
body {
    font-family: Arial;
    background-color: #f5f5f5;
}

h1 {
    color: blue;
}
```
