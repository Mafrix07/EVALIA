# Evalia

Plateforme académique de création et de passage de QCM assistée par IA, avec correction côté serveur, gestion de quotas pour les enseignants et mode de remédiation pour les étudiants.

---

## Architecture

- **Backend** : Django 5 / Django REST Framework (authentification JWT, gestion des quotas, intégration Gemini ou mock local).
- **Frontend** : React 18 / TypeScript / Tailwind CSS avec Vite.

```
evalia/
├── backend/          # API Django REST Framework
│   ├── accounts/     # Utilisateurs, rôles, quotas
│   ├── quizzes/      # Gestion et publication des QCM
│   ├── attempts/     # Passages, notation et remédiation
│   └── ai_generator/ # Intégration Gemini & FinOps
└── src/              # Application React / Vite
```

---

## Prérequis

- Python 3.11+
- Node.js 18+

---

## Installation et démarrage

### 1. Backend (Django)

```bash
cd backend

# Créer et activer l'environnement virtuel
python -m venv .venv
# Sur Windows :
.venv\Scripts\activate
# Sur Linux/macOS :
# source .venv/bin/activate

# Installer les dépendances
pip install -r requirements.txt

# Initialiser la base et charger les données de démo
python manage.py migrate
python manage.py seed_evalia

# Lancer le serveur d'API (http://127.0.0.1:8000)
python manage.py runserver
```

> **Note :** Par défaut, le backend démarre sur SQLite et utilise un générateur de QCM local sans clé API. Pour activer le modèle Gemini réel, définissez `GEMINI_API_KEY` dans `backend/.env`.

### 2. Frontend (React / Vite)

Dans un second terminal, à la racine du projet :

```bash
# Installer les dépendances
npm install

# Démarrer le serveur de développement (http://localhost:5173)
npm run dev
```

---

## Comptes de démonstration

La commande `python manage.py seed_evalia` crée automatiquement des comptes prêts à l'emploi :

| Rôle | Email | Mot de passe | Description |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@evalia.local` | `Admin12345!` | Validation profs, supervision des coûts |
| **Enseignant** | `marie.teacher@evalia.local` | `Teacher12345!` | Génération de QCM, gestion des examens |
| **Enseignant (en attente)** | `paul.pending@evalia.local` | `Teacher12345!` | Compte soumis à validation admin |
| **Étudiant** | `lea.student@evalia.local` | `Student12345!` | Passage des QCM et remédiation |

Un QCM de démonstration est accessible avec le code **`EXAM2026`**.

---

## Configuration (`.env`)

Des fichiers `.env.example` sont disponibles à la racine et dans `backend/` :

- **`backend/.env`** :
  - `DJANGO_SECRET_KEY` : Clé secrète de l'application
  - `DJANGO_DEBUG` : Mode débogage (`true` / `false`)
  - `GEMINI_API_KEY` : Clé API Google AI Studio (optionnelle)
  - `CORS_ALLOWED_ORIGINS` : Origines autorisées pour le frontend
- **`.env` (racine)** :
  - `VITE_API_URL` : URL de l'API (par défaut `http://127.0.0.1:8000/api`)

---

## Tests backend

Pour lancer la suite de tests automatisés :

```bash
cd backend
python manage.py test
```
