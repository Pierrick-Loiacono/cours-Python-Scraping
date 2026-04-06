# Environnement virtuel

### 1. Vue d'ensemble

Un environnement virtuel permet de créer un espace isolé pour un projet Python. Sans environnement virtuel (venv) toutes les bibliothèques sont installées globalement et peut donc entrainer des conflits avec d'autre projet mais aussi entraine une difficulté à partager le projet.

Avec un environnement virtuel (venv) :
- chaque projet a ses propres dépendances
- n'interfère pas avec d'autre projet
- environnement reproductible sur d'autre machine

### 2. Création et activation de l'environnement virtuel

#### Création
La commande suivante créera un dossier **`venv`** à la racine de votre projet (pensez à être dans le bon dossier)

```bash
python -m venv venv
```

#### Activation

La commande diffère si vous êtes sur Windows ou Linux / Mac

**Windows**
```bash
venv\Scripts\activate
```

**Linux / Mac**
```bash
source venv/bin/activate
```

Pour vérifier que l'environnement virtuel est bien activé, il suffit de regarder le terminal

```bash
(venv) PS C:\Users\Pierr\projetDev\python-scrapping>
```

Une fois activé vous pouvez installer les dépendances nécessaires à votre projet, ils iront directement dans ce dossier et non plus dans l'installation global

### 3. Sauvegarder les dépendances

Sans surprise, comme dans tous les projets, on n'envoie jamais directement le dossier de dépendance sur GitHub ou autre, pourquoi ? Parce le dossier est trop lourd et dépend du système

Pour faire bien, vous pouvez extraire les dépendances dans un fichier texte qui sera partagé avec tout le monde, et chacun pourra les installer.

#### Extraire les dépendances 

```bash
pip freeze > requirements.txt
```

#### Recréer l'environnement sur une autre machine

```bash
python -m venv venv
venv\Scripts\activate # propre a Windows

pip install -r requirements.txt
```

### 4. Quitter un environnement virtuel

```bash
deactivate
```

### 5. Résumé
Un environnement virtuel permet d’isoler les dépendances d’un projet Python.
Il ne doit pas être versionné, mais peut être recréé facilement à partir d’un fichier **requirements.txt**.

---


