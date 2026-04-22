# 🎵 Drive Player — Lecteur MP3 Google Drive

Application web statique (1 seul fichier HTML) hébergeable sur **GitHub Pages**.  
Lis et joue vos fichiers MP3 stockés sur Google Drive, directement dans le navigateur.

---

## ✨ Fonctionnalités

- 🎵 Lecture de fichiers MP3 depuis Google Drive (via OAuth 2.0)
- 📁 Filtrage par dossier Drive spécifique (optionnel)
- 📂 Lecture de fichiers locaux (drag & drop / parcourir)
- 🔀 Mode aléatoire + 🔁 Répétition (une piste / tout)
- 🔍 Recherche dans la playlist
- ⌨️ Raccourcis clavier (Espace = play/pause, ← → = précédent/suivant)
- 💾 Configuration sauvegardée en localStorage

---

## 🚀 Déploiement sur GitHub Pages

### Étape 1 — Créer le dépôt

```bash
git init drive-player
cd drive-player
cp /path/to/index.html .
git add index.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/VOTRE_USERNAME/drive-player.git
git push -u origin main
```

Ensuite dans **Settings → Pages → Source** : sélectionner `main` / `root`.

Votre URL sera : `https://VOTRE_USERNAME.github.io/drive-player/`

---

## 🔧 Configuration Google Cloud Console

### 1. Créer un projet

1. Aller sur [console.cloud.google.com](https://console.cloud.google.com)
2. **Nouveau projet** → nommer "Drive Player"

### 2. Activer l'API Google Drive

1. **APIs & Services → Bibliothèque**
2. Rechercher "Google Drive API" → **Activer**

### 3. Créer les identifiants OAuth 2.0

1. **APIs & Services → Identifiants → Créer des identifiants → ID client OAuth 2.0**
2. Type d'application : **Application web**
3. Origines JavaScript autorisées :
   ```
   https://VOTRE_USERNAME.github.io
   http://localhost:8080   ← pour les tests locaux
   ```
4. Copier le **Client ID** généré

### 4. Configurer l'écran de consentement OAuth

1. **APIs & Services → Écran de consentement OAuth**
2. Type : **Externe**
3. Remplir : nom de l'app, e-mail
4. Scopes : ajouter `drive.readonly`
5. Ajouter votre adresse e-mail comme **utilisateur test**

---

## ⚙️ Configuration dans l'app

Au premier lancement, la fenêtre de configuration s'ouvre automatiquement.  
Renseigner :

| Champ | Description |
|-------|-------------|
| **Client ID** | ID OAuth 2.0 de Google Cloud Console |
| **API Key** | Optionnelle (pour fichiers publics uniquement) |
| **ID du dossier** | ID du dossier Drive souhaité (laisser vide = tout Drive) |

> 💡 **Trouver l'ID d'un dossier Drive** : ouvrir le dossier dans Drive, copier la partie après `/folders/` dans l'URL.

---

## 🎹 Raccourcis clavier

| Touche | Action |
|--------|--------|
| `Espace` | Play / Pause |
| `→` | Piste suivante |
| `←` | Piste précédente |

---

## 📁 Structure

```
drive-player/
└── index.html    ← Tout en un seul fichier
```

---

## 🔒 Sécurité & Confidentialité

- Aucune donnée n'est envoyée à un serveur tiers
- L'authentification OAuth se fait directement entre votre navigateur et Google
- Le token d'accès n'est jamais persisté (session uniquement)
- Les fichiers MP3 sont streamés directement depuis Drive vers votre navigateur

---

## 🛠️ Test en local

```bash
# Python 3
python -m http.server 8080
# Ouvrir : http://localhost:8080
```
