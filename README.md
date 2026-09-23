# ✈️ Gestion d’un aéroport — Base de données

Projet de modélisation d’une base de données consacré au fonctionnement d’un aéroport. Il présente l’analyse du domaine, le modèle conceptuel de données (MCD), le modèle logique de données (MLD) et la documentation associée.

> Projet pédagogique réalisé à l’ETML dans le cadre du module de bases de données.

## 🎯 Objectifs

Ce projet a pour but de concevoir une base de données cohérente permettant de représenter les principales informations nécessaires à la gestion d’un aéroport.

Les objectifs sont notamment de :

- analyser un cahier des charges et identifier les données utiles ;
- déterminer les entités, leurs attributs et leurs relations ;
- définir les cardinalités et les règles de gestion ;
- construire un MCD clair et normalisé ;
- transformer le MCD en MLD ;
- préparer la future création de la base de données et des requêtes SQL ;
- documenter les choix de conception.

## 🛫 Domaine étudié

La modélisation couvre le fonctionnement général d’un environnement aéroportuaire. Elle permet d’organiser les informations liées aux différents éléments du domaine et leurs interactions.

Le modèle est conçu afin de :

- limiter la duplication des données ;
- garantir la cohérence des relations ;
- faciliter la recherche et la mise à jour des informations ;
- servir de base à une implémentation relationnelle en SQL.

## 🧩 Démarche de conception

### 1. Analyse du besoin

Le cahier des charges est étudié afin d’identifier les objets métier, les informations à conserver et les contraintes à respecter.

### 2. Modèle conceptuel de données — MCD

Le MCD représente les entités du système, leurs propriétés, leurs associations et leurs cardinalités, indépendamment du système de gestion de base de données utilisé.

### 3. Modèle logique de données — MLD

Le MLD traduit le modèle conceptuel sous une forme relationnelle exploitable :

- création des tables ;
- définition des clés primaires ;
- ajout des clés étrangères ;
- traduction des relations entre les entités ;
- préparation des contraintes d’intégrité.

### 4. Implémentation SQL

L’étape suivante consiste à générer ou écrire le schéma SQL, insérer des données de test et réaliser les requêtes demandées. Les scripts SQL seront ajoutés au dépôt lorsqu’ils seront finalisés.

## 📁 Structure du dépôt

```text
P_DB_GestionAeroport/
├── MCD-MLD/
│   └── gestionAeroport.loo
├── doc/
│   ├── E-P_DB-GCR001-CdC-2026.pdf
│   └── src/
│       ├── AugustoRomain-P_DB_GestionAeroport-Rapport.docx
│       └── E-P_DB-GCR001-CdC-2026.docx
└── README.md
```

| Élément | Description |
|---|---|
| `gestionAeroport.loo` | Modèle de données éditable avec Looping |
| `E-P_DB-GCR001-CdC-2026.pdf` | Cahier des charges du projet |
| `AugustoRomain-P_DB_GestionAeroport-Rapport.docx` | Rapport et justification du travail réalisé |
| `E-P_DB-GCR001-CdC-2026.docx` | Version modifiable du cahier des charges |

> Les fichiers dont le nom commence par `~$` sont des fichiers temporaires créés automatiquement par Microsoft Word et ne font pas partie de la documentation principale.

## 🛠️ Outils

- **Looping** pour créer et modifier le MCD/MLD ;
- **Microsoft Word** ou un logiciel compatible pour consulter les sources de la documentation ;
- un lecteur **PDF** pour lire le cahier des charges exporté ;
- un **SGBD relationnel** et un client SQL pour la future implémentation.

## 🚀 Consulter le projet

1. Cloner le dépôt :

```bash
git clone https://github.com/Pt74bsx/P_DB_GestionAeroport.git
```

2. Ouvrir le dossier du projet :

```bash
cd P_DB_GestionAeroport
```

3. Installer Looping si nécessaire.
4. Ouvrir `MCD-MLD/gestionAeroport.loo`.
5. Consulter le cahier des charges dans `doc/`.
6. Lire le rapport disponible dans `doc/src/`.

## ✅ État du projet

- [x] Analyse initiale du cahier des charges
- [x] Création du modèle de données avec Looping
- [x] Ajout de la documentation du projet
- [x] Rédaction du rapport
- [ ] Finalisation et validation du modèle
- [ ] Ajout du schéma SQL
- [ ] Ajout de données de démonstration
- [ ] Création des requêtes SQL
- [ ] Documentation des résultats

## 🔮 Améliorations prévues

- exporter une image du MCD pour permettre une consultation directe sur GitHub ;
- ajouter les scripts de création des tables ;
- documenter chaque table, clé et contrainte ;
- fournir un jeu de données de test ;
- ajouter des exemples de requêtes SQL ;
- nettoyer les fichiers temporaires générés par les logiciels bureautiques.

## 👤 Auteur

**Romain Augusto**  
Étudiant développeur à l’ETML

[Voir le profil GitHub](https://github.com/Pt74bsx)
