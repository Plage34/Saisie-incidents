# 📋 Incidents Scolaires - Application Mobile

Application mobile de saisie d'incidents scolaires, conçue pour fonctionner sur **iPhone** et **Android** via un navigateur web. Elle génère un fichier JSON qui est transmis par email pour être intégré à l'application principale de gestion des incidents.

## 📱 Fonctionnalités

- **Saisie guidée en 4 étapes** : Quand/Où → Qui → Quoi → Mesures & Envoi
- **Listes pré-configurées** synchronisées avec l'application principale (lieux, natures, classes, enseignants, mesures, suites)
- **Prise de photo** directe depuis l'appareil ou la galerie
- **Sélecteur de gravité** (Faible / Moyenne / Grave)
- **Génération automatique** d'un fichier JSON compatible avec le parser d'import
- **Envoi par email** via l'application mail native du téléphone
- **Historique local** des incidents saisis avec possibilité de renvoi
- **Mode hors-ligne** (PWA installable sur l'écran d'accueil)
- **Interface sombre** optimisée pour mobile

## 🚀 Installation sur GitHub Pages

### 1. Créer le dépôt GitHub

```bash
# Cloner ou créer un nouveau dépôt
git init incidents-scolaires-mobile
cd incidents-scolaires-mobile

# Copier les fichiers
cp index.html manifest.json sw.js icon-192.png icon-512.png ./

# Premier commit
git add .
git commit -m "Initial: application mobile saisie incidents"
git branch -M main
git remote add origin https://github.com/VOTRE-COMPTE/incidents-scolaires-mobile.git
git push -u origin main
```

### 2. Activer GitHub Pages

1. Allez dans **Settings** → **Pages** de votre dépôt
2. Source : sélectionnez **Deploy from a branch**
3. Branch : **main** / **/ (root)**
4. Cliquez **Save**
5. Attendez quelques minutes, votre app sera accessible à :
   `https://VOTRE-COMPTE.github.io/incidents-scolaires-mobile/`

### 3. Installer sur le téléphone (optionnel mais recommandé)

**iPhone (Safari)** :
1. Ouvrir l'URL dans Safari
2. Appuyer sur le bouton **Partager** (carré avec flèche)
3. Choisir **Sur l'écran d'accueil**
4. Confirmer → L'icône apparaît sur votre écran

**Android (Chrome)** :
1. Ouvrir l'URL dans Chrome
2. Menu ⋮ → **Ajouter à l'écran d'accueil**
3. Confirmer → L'icône apparaît sur votre écran

## 📧 Workflow d'envoi

```
┌──────────────┐    ┌──────────┐    ┌──────────────────┐
│  App Mobile  │───▶│  Email   │───▶│  App Principale  │
│  (téléphone) │    │ (JSON)   │    │  (PC / bureau)   │
└──────────────┘    └──────────┘    └──────────────────┘
     Saisie        Transmission         Import auto
```

1. L'enseignant saisit l'incident sur son téléphone
2. Un fichier `incident_YYYY-MM-DDTHH-MM-SS.json` est téléchargé
3. L'application mail s'ouvre avec le sujet `[INCIDENT MOBILE]`
4. L'enseignant **joint le fichier JSON** et envoie le mail
5. L'application principale importe automatiquement les incidents depuis la boîte mail

## 🔄 Import dans l'application principale

Le fichier `mobile_email_parser_v2.py` remplace l'ancien `mobile_email_parser.py` dans l'application principale. Il est **rétro-compatible** avec l'ancien format.

### Mise à jour du parser

1. Copier `mobile_email_parser_v2.py` dans le dossier de l'application principale
2. Renommer en `mobile_email_parser.py` (remplacer l'ancien)
3. Relancer l'application

### Format JSON généré (v2)

```json
{
    "date_incident": "20/02/2026",
    "heure": "10:30",
    "auteurs": "DUPONT Marie",
    "victimes": "MARTIN Paul",
    "nom_complet_eleve": "DUPONT Marie",
    "classe": "CM2 FERMIER Christelle",
    "lieu_exact": "Cour de récréation",
    "nature_incident": "Dispute / bagarre",
    "description_detaille": "Description de l'incident...",
    "personnel_temoin": "FORESTIER Estelle",
    "mesures_prises": "Séparation élèves, Famille contactée",
    "suites_donnees": "Convocation famille auteur",
    "enseignant": "FERMIER Christelle",
    "gravite": "Moyenne",
    "enregistre_le": "20/02/2026 10:35:00",
    "source": "Application Mobile"
}
```

## ⚙️ Personnalisation des listes

Les listes déroulantes (lieux, natures, classes, etc.) sont définies dans la constante `CONFIG` du fichier `index.html`. Pour les modifier :

1. Ouvrir `index.html` dans un éditeur de texte
2. Chercher `const CONFIG = {`
3. Modifier les tableaux selon vos besoins
4. Sauvegarder et pousser sur GitHub

```javascript
const CONFIG = {
    lieux: ["Salle de classe", "Cour de récréation", ...],
    natures: ["Blessure", "Dispute / bagarre", ...],
    classes: ["CP BARTHELEMY Nathalie", ...],
    enseignants: ["GILLET Virginie", ...],
    // ...
};
```

## 📁 Structure du projet

```
incidents-scolaires-mobile/
├── index.html                    # Application complète (HTML/CSS/JS)
├── manifest.json                 # Manifest PWA
├── sw.js                         # Service Worker (mode hors-ligne)
├── icon-192.png                  # Icône PWA 192x192
├── icon-512.png                  # Icône PWA 512x512
├── mobile_email_parser_v2.py     # Parser mis à jour (pour l'app principale)
└── README.md                     # Ce fichier
```

## 🔐 Données et confidentialité

- **Aucune donnée n'est envoyée à un serveur** : tout reste sur le téléphone
- L'historique local utilise le `localStorage` du navigateur
- Les données sont transmises uniquement par email, sous votre contrôle
- Le fichier JSON ne contient que les informations saisies dans le formulaire

## 📋 Compatibilité

| Navigateur | Version min. | Statut |
|------------|-------------|--------|
| Safari iOS | 14+ | ✅ Testé |
| Chrome Android | 90+ | ✅ Testé |
| Firefox Android | 90+ | ✅ Compatible |
| Samsung Internet | 15+ | ✅ Compatible |

---

*Application développée pour compléter le système de Gestion des Incidents Scolaires.*
