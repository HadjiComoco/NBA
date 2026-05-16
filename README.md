# 🏀 Application de suivi des Playoffs NBA 2024-2025

> Projet universitaire réalisé dans le cadre du cours de Base de Données 2 — L2 MIASHS  
> Hadji HAMADA — Année universitaire 2024-2025

---

## 📋 Description

Application de bureau développée sous **Microsoft Access** permettant de gérer et consulter les données des **Playoffs NBA 2024-2025**. Elle s'adresse aux passionnés de basketball souhaitant explorer les statistiques des équipes, joueurs et matchs de la phase finale de la saison NBA.

---

## 🗃️ Base de données

### Modèle Conceptuel (MCD)
- **3 entités** : `Joueur`, `Equipe`, `Match`
- **1 association porteuse d'attributs** : `Joue` (points, note)
- **Cardinalités** : 1,1 — 1,n entre Joueur et Equipe / 0,n — 0,n entre Joueur et Match

### Modèle Logique (MLD)
| Table | Champs principaux |
|-------|-------------------|
| `Equipe` | id_equipe (CP), nom, ville, logo, conference |
| `Joueur` | id_joueur (CP), nom, prenom, poste, nationalite, date_naissance, photo, #id_equipe |
| `Match` | id_match (CP), date, lieu, score, saison, #id_equipe_dom, #id_equipe_ext |
| `Joue` | #id_joueur, #id_match (CP composée), points, note |

### Données
- 🏀 **16 équipes** qualifiées aux Playoffs 2025
- 👤 **160 joueurs** (10 titulaires par équipe — roster officiel NBA)
- 🏟️ **30 matchs** du 1er tour des Playoffs 2025
- 📊 **120+ performances** de joueurs (table Joue)

---

## 💻 Fonctionnalités de l'application

| Formulaire / État | Type | Description |
|---|---|---|
| `F_Accueil` | Menu général | Point d'entrée unique vers toutes les fonctionnalités |
| `F_Equipes` | Formulaire simple | Consultation et gestion des 16 équipes (avec logo) |
| `F_Joueurs` | Formulaire + sous-formulaire | Roster complet par équipe |
| `F_Match` | Formulaire simple | Consultation des résultats de matchs |
| `F_Recherche_Joueurs` | Recherche multicritères | Filtrage par équipe, poste et nationalité |
| `F_Recherche_Matchs` | Recherche multicritères | Filtrage par équipe et période de dates |
| `E_Stats_Joueurs` | État imprimable | Classement des joueurs par note et points moyens |

---

## 🛠️ Technologies utilisées

- **Microsoft Access** — Création des tables, relations, formulaires et états
- **SQL** — Requêtes de sélection, jointures, agrégats (SUM, AVG, GROUP BY)
- **VBA (Visual Basic for Applications)** — Filtres dynamiques multicritères, import de données par scripts
- **Modélisation relationnelle** — MCD (Entité-Association), MLD, règles de transformation

---

## 📁 Structure du projet

```
ProjetNBA/
├── Nba_hadji.accdb        # Base de données Access (tables + application)
├── NBA_2024_2025.sql      # Script SQL d'insertion des données
├── Rapport_NBA.pdf        # Rapport technique complet
└── README.md
```

---

## 🚀 Installation et utilisation

1. **Cloner le dépôt**
```bash
git clone https://github.com/username/ProjetNBA.git
```

2. **Ouvrir le fichier**
   - Ouvrir `Nba_hadji.accdb` avec **Microsoft Access 2016 ou version ultérieure**
   - Activer le contenu si demandé (macros et VBA)

3. **Lancer l'application**
   - Le formulaire `F_Accueil` s'ouvre automatiquement
   - Naviguer via les boutons du menu

> ⚠️ **Prérequis** : Microsoft Access 2016+ (Windows uniquement)

---

## 📊 Exemple de requête SQL

Classement des meilleurs joueurs par note moyenne :

```sql
SELECT 
    Joueur.nom,
    Joueur.prenom,
    Equipe.nom AS equipe,
    Joueur.poste,
    Sum(Joue.points) AS total_points,
    Round(Avg(Joue.points), 1) AS moy_points,
    Round(Avg(Joue.note), 1) AS moy_note
FROM (Joueur 
INNER JOIN Joue ON Joueur.id_joueur = Joue.id_joueur)
INNER JOIN Equipe ON Joueur.id_equipe = Equipe.id_equipe
GROUP BY Joueur.nom, Joueur.prenom, Equipe.nom, Joueur.poste
ORDER BY Avg(Joue.note) DESC;
```

---

## 👥 Auteurs

- **Hadji HAMADA** — L2 MIASHS

---

## 📄 Licence

Projet universitaire — Usage académique uniquement.
