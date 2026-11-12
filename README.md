# DocTutor – Projet Web (Objectif 3)

**Groupe 12 – SUP'COM – Année universitaire 2025/2026**
Encadrante : Dr. Maroua Nouioua
Membres du groupe : Koussay Abd Essamai Massoudi

## 1. Présentation

DocTutor est une plateforme web de consultation de cours et de tutoriels PDF.
Un étudiant consulte les tutoriels publiés. Un administrateur gère le catalogue de cours et de tutoriels.

## 2. Choix du framework et des technologies

| Couche | Technologie | Pourquoi ce choix |
|---|---|---|
| Frontend | Angular 14 | Composants réutilisables, routage intégré, service HTTP, structure claire |
| Backend | Node.js, Express, Sequelize | API REST légère et simple à héberger |
| Base de données | PostgreSQL sur Supabase | Base relationnelle gratuite hébergée dans le cloud |
| Stockage des PDF | Supabase Storage | Fichiers accessibles par lien public |
| Hébergement du backend | Render | Déploiement automatique depuis GitHub |

Le projet est parti d'un exemple CRUD Angular + Node.js (bezkoder.com), adapté et étendu : rôles, cours, tutoriels liés à un cours, publication et envoi de PDF.

## 3. Fonctionnalités développées

- Choix du rôle : espace étudiant ou espace administrateur
- Catalogue de cours, puis liste des tutoriels de chaque cours
- Détail d'un tutoriel
- **Étudiant** : consulte les tutoriels publiés et ouvre le PDF
- **Administrateur** :
  - ajouter un cours
  - ajouter un tutoriel dans un cours, avec un fichier PDF
  - modifier et supprimer un tutoriel
  - publier ou dépublier un tutoriel
- API REST : `GET`, `POST`, `PUT`, `DELETE` sur `/api/tutorials`

> L'accès administrateur est protégé par un simple code côté client. C'est une simplification pour la démonstration : une application réelle utiliserait une authentification côté serveur.

## 4. Structure du projet

```
Doctutor/
├── angular-14-client/          Frontend Angular
│   └── src/app/
│       ├── components/         role-selection, home, tutorials-list,
│       │                       tutorial-details, add-course, add-tutorial
│       ├── models/
│       └── services/           tutorial.service.ts (appels HTTP)
└── node-js-server/             Backend Express
    ├── server.js
    └── app/                    config, controllers, models, routes
```

## 5. Lancement du projet

### Prérequis
Node.js (version LTS) et npm.

### Backend

```bash
cd node-js-server
npm install
```

Définir les variables d'environnement de la base Supabase, puis démarrer le serveur.
Exemple sous PowerShell :

```powershell
$env:DB_HOST='<hôte Supabase>'
$env:DB_USER='<utilisateur>'
$env:DB_PASSWORD='<mot de passe>'
node server.js
```

Le serveur démarre sur http://localhost:8080.

Un backend est aussi déployé en ligne : https://doctutor-backend.onrender.com/api/tutorials
(l'hébergement gratuit se met en veille : la première requête peut prendre environ une minute).

### Frontend

```bash
cd angular-14-client
npm install
ng serve
```

Ouvrir http://localhost:4200.
L'adresse de l'API se règle dans `src/environments/environment.ts`.

### Accès administrateur
Sur la page d'accueil, choisir « Espace administrateur » et saisir le code de démonstration communiqué à l'encadrante.

## 6. Tests réalisés

- Navigation entre toutes les pages
- Ajout, modification, suppression et publication d'un tutoriel
- Envoi et ouverture d'un PDF
- Comportement du site avec le backend en ligne