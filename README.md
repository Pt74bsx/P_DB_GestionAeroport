# ✈️ Gestion d’un aéroport — SkyConnect

Projet individuel de bases de données réalisé à l’**ETML** par **Romain Augusto**, du **24 août au 28 octobre 2026**, dans le cadre du projet **P_DB** et des modules **106, 162 et 164**.

L’objectif est de concevoir et d’exploiter une base de données relationnelle pour l’aéroport fictif **SkyConnect** : compagnies aériennes, avions, programmes de vol, vols réels, passagers et réservations. Le travail couvre la modélisation avec **MERISE et Looping**, l’implémentation sous **MySQL**, le chargement de fichiers **TSV** et l’écriture de requêtes SQL.

> **Avancement au 28 octobre 2026 :** le rapport présente le MCD, le MLD, la création de `db_aeroport`, les huit imports TSV et les requêtes SQL 1 à 5. Les requêtes suivantes, les index, les rôles et les transactions restent à compléter dans le rapport.

## Sommaire

- [Périmètre et modèle de données](#périmètre-et-modèle-de-données)
- [Travail demandé et avancement](#travail-demandé-et-avancement)
- [Organisation du dépôt](#organisation-du-dépôt)
- [Outils et prérequis](#outils-et-prérequis)
- [Prise en main](#prise-en-main)
- [Chargement des données](#chargement-des-données)
- [Requêtes SQL](#requêtes-sql)
- [Prochaines étapes](#prochaines-étapes)
- [Auteur et documentation](#auteur-et-documentation)

## Périmètre et modèle de données

La base distingue le **programme de vol**, qui définit une liaison régulière avec des jours et des horaires prévus, du **vol réel**, qui correspond à une date et à un avion précis. Les aéroports de départ et d’arrivée d’un vol réel peuvent différer de ceux de son programme.

| Élément | Informations et relations principales |
| --- | --- |
| Aéroport | Nom, code IATA et code ICAO ; aéroport de départ, d’arrivée ou base d’une compagnie |
| Compagnie aérienne | Nom, code IATA et aéroport principal ; possède des avions et exploite des vols |
| Type d’avion | Modèle et description d’un appareil |
| Avion | Appareil appartenant à une compagnie et rattaché à un type ; capacité propre à chaque avion |
| Programme de vol | Numéro de vol, compagnie, trajet et horaires prévus |
| Jour de semaine | Fréquence hebdomadaire des programmes, identifiée dans l’analyse du rapport |
| Vol | Date, horaires, avion, compagnie, aéroports de départ et d’arrivée, programme associé |
| Passager | Nom, prénom et numéro de passeport unique |
| Réservation | Association entre un passager et un vol, avec un siège et un prix |

Les relations reposent sur des clés primaires et étrangères. Une réservation dépend d’un passager et d’un vol ; un avion dépend d’une compagnie et d’un type d’avion. Ces dépendances déterminent notamment l’ordre de chargement des données.

## Travail demandé et avancement

L’état ci-dessous correspond au contenu du rapport fourni, mis à jour le **28.10.2026**.

| Étape du cahier des charges | État documenté |
| --- | --- |
| Analyse du domaine, dictionnaire des données, règles et cardinalités | Présentés dans le rapport |
| MCD et MLD avec Looping | Présentés dans le rapport ; validation par l’enseignant requise avant l’implémentation selon le CdC |
| Création des tables dans `db_aeroport` | Réalisée et illustrée avec phpMyAdmin |
| Chargement des données avec `LOAD DATA INFILE` | Huit imports documentés, avec captures d’exécution |
| 15 requêtes SQL et explications techniques | Requêtes 1 à 5 rédigées ; requête 6 commencée, sans SQL ; requêtes 7 à 15 à ajouter |
| Choix et création des index pour les deux requêtes imposées | Section à compléter |
| Rôles, privilèges et au moins un utilisateur par rôle | Section à compléter |
| Transactions : annulation d’un vol et analyse du cas fourni | Section à compléter |
| Utilisation de l’IA | Aides déjà mentionnées dans le texte ; section récapitulative à compléter |
| Conclusion | À rédiger |

## Organisation du dépôt

| Dossier / fichier | Contenu ou utilisation |
| --- | --- |
| `BDD/` | Sauvegardes SQL de la base de données |
| ↳ `db_aeroport2026.10.06.sql` | Sauvegarde du 6 octobre 2026 |
| ↳ `db_aeroport2026.10.07.sql` | Sauvegarde du 7 octobre 2026 |
| ↳ `db_aeroport2026.10.26.sql` | Sauvegarde du 26 octobre 2026, la plus récente affichée |
| `DOC/` | Documentation du projet |
| ↳ `E-P_DB-GCR001-CdC-2026.pdf` | Cahier des charges au format PDF |
| `DOC/annexes/` | Rapport Word du projet et fichier de requêtes |
| ↳ `requete.txt` | Fichier texte des requêtes |
| `DOC/img/` | Captures utilisées pour documenter le projet |
| ↳ `1.CreationDB/` | Captures de création de la base |
| ↳ `2.ChargementDonnees/` | Captures de chargement des données |
| `DOC/src/` | Documents sources et conventions de codage |
| ↳ `E-P_DB-GCR001-CdC-2026.docx` | Version Word du cahier des charges |
| ↳ `I-ConventionsDeCodageV3.6.0.pdf` | Conventions de codage de l’ETML |
| `MCD-MLD/` | Modèle de données du projet |
| ↳ `db_aeroport.loo` | Modèle principal à ouvrir dans Looping |
| ↳ `db_aeroport.lo1` | Fichier complémentaire du modèle Looping |
| `MCD-MLD/Données-Projet-Aeroport/` | Modèle fourni avec les données et fichiers TSV |
| ↳ `aéroport.loo` | Modèle Looping présent dans les données du projet |
| ↳ `t_aeroport.tsv` | Données des aéroports |
| ↳ `t_avion.tsv` | Données des avions |
| ↳ `t_compagnie.tsv` | Données des compagnies aériennes |
| ↳ `t_passager.tsv` | Données des passagers |
| ↳ `t_programme_vol.tsv` | Données des programmes de vol |
| ↳ `t_reservation.tsv` | Données des réservations |
| ↳ `t_type_avion.tsv` | Données des types d’avion |
| ↳ `t_vol.tsv` | Données des vols |
| `.gitattributes` | Règles Git, notamment le suivi des fichiers avec Git LFS |
| `README.md` | Présentation et prise en main du projet |

Le rapport Word se trouve dans **`DOC/annexes/`**. Le modèle principal est **`MCD-MLD/db_aeroport.loo`**. Conserver la casse et les accents des chemins, notamment `DOC/` et `Données-Projet-Aeroport/`.

## Outils et prérequis

- **Looping** : consulter et modifier le MCD et le MLD.
- **Docker et MySQL** : environnement de base de données prévu par le cahier des charges.
- **phpMyAdmin** ou un client **MySQL** : exécuter le SQL et consulter les tables.
- **Git et Git LFS** : récupérer le dépôt et les fichiers suivis avec LFS.
- Un lecteur **PDF** et un logiciel compatible **Word** : consulter le cahier des charges et le rapport.

Les règles Git LFS fournies couvrent notamment `BDD/` et `MCD-MLD/Données-Projet-Aeroport/`. Un fichier SQL contenant uniquement un pointeur LFS doit être téléchargé avec Git LFS avant d’être importé.

## Prise en main

### 1. Récupérer le projet

```bash
git lfs install
git clone https://github.com/Pt74bsx/P_DB_GestionAeroport.git
cd P_DB_GestionAeroport
git lfs pull
```

### 2. Consulter la conception

Lire le cahier des charges dans `DOC/`, puis le rapport Word dans `DOC/annexes/`. Ouvrir `MCD-MLD/db_aeroport.loo` dans Looping pour consulter les entités, les associations, les cardinalités et la traduction relationnelle.

### 3. Préparer MySQL

Démarrer l’environnement MySQL et phpMyAdmin utilisé pour le projet. Les noms de conteneurs, les ports et les identifiants dépendent de l’environnement local.

Deux possibilités permettent de préparer la base :

- **Restaurer une sauvegarde** : choisir l’export SQL voulu dans `BDD/` et l’importer avec phpMyAdmin ou le client MySQL. Vérifier si l’export crée et sélectionne déjà la base.
- **Reconstruire depuis le modèle** : créer `db_aeroport`, y exécuter le schéma MySQL généré par Looping, puis charger les TSV dans l’ordre indiqué ci-dessous.

Effectuer la restauration dans une base de travail : un export peut contenir des instructions de suppression ou de recréation des tables. Ne pas recharger les TSV si la sauvegarde contient déjà les données.

## Chargement des données

Les huit fichiers TSV sont disponibles dans `MCD-MLD/Données-Projet-Aeroport/`.

Le rapport utilise **`LOAD DATA INFILE`**, qui lit les fichiers depuis le serveur MySQL. Dans l’environnement présenté, les fichiers TSV sont placés dans **`/var/lib/mysql-files/`**. Avec Docker, ce chemin doit être accessible **dans le conteneur MySQL**.

Vérifier le répertoire autorisé avant l’import :

```sql
SHOW VARIABLES LIKE 'secure_file_priv';
```

### Ordre des imports et volumes observés

Les captures du rapport montrent les volumes suivants, avec **0 ligne ignorée (`Skipped`) et 0 avertissement (`Warnings`)** pour chacun de ces huit imports.

| Ordre | Fichier TSV | Table cible | Lignes importées |
| --- | --- | --- | ---: |
| 1 | `t_aeroport.tsv` | `t_aeroport` | 9 854 |
| 2 | `t_compagnie.tsv` | `t_compagnie` | 110 |
| 3 | `t_type_avion.tsv` | `t_type_avion` | 342 |
| 4 | `t_avion.tsv` | `t_avion` | 3 950 |
| 5 | `t_passager.tsv` | `t_passager` | 36 095 |
| 6 | `t_programme_vol.tsv` | `t_programme_vol` | 9 614 |
| 7 | `t_vol.tsv` | `t_vol` | 321 911 |
| 8 | `t_reservation.tsv` | `t_reservation` | 5 455 883 |

Importer les tables parentes avant les tables qui les référencent évite les erreurs de clé étrangère, notamment pour les avions et les réservations.

### Cas particulier des codes d’aéroport

Certains champs du TSV contiennent le texte `NULL`. Le rapport utilise des variables intermédiaires et `NULLIF` pour le convertir en valeur SQL `NULL` :

```sql
USE db_aeroport;

LOAD DATA INFILE '/var/lib/mysql-files/t_aeroport.tsv'
INTO TABLE t_aeroport
CHARACTER SET utf8mb4
FIELDS TERMINATED BY '\t'
LINES TERMINATED BY '\n'
IGNORE 1 LINES
(aeroport_id, @iata, @icao, nom)
SET
    code_iata = NULLIF(@iata, 'NULL'),
    code_icao = NULLIF(@icao, 'NULL');
```

Les colonnes concernées doivent accepter `NULL`. Cette conversion évite notamment de tenter d’insérer les quatre caractères du texte `NULL` dans un code IATA limité à trois caractères. Les commandes des autres imports et leurs captures figurent dans le rapport.

## Requêtes SQL

Le cahier des charges impose **15 requêtes**, accompagnées d’explications sur les clauses et techniques utilisées.

| N° | Objectif | Présence dans le rapport |
| --- | --- | --- |
| 1 | Deux avions de la compagnie 60, par capacité décroissante | SQL et résultat |
| 2 | Trois vols avec l’heure de départ la plus tardive | SQL et résultat |
| 3 | Nombre de vols par compagnie | SQL et résultat |
| 4 | Passagers, passeports et aéroports de départ des vols réservés | SQL et résultat |
| 5 | Prix moyen des réservations par vol | SQL et résultat |
| 6 | Tous les aéroports et leurs compagnies, y compris sans compagnie | Énoncé présent ; SQL à compléter |
| 7–10 | Nombre d’avions, compagnies ayant au moins 1 500 vols, vols par compagnie et aéroport, capacités par compagnie et type | À ajouter |
| 11–12 | Compagnies sans avion avec une sous-requête ; programmes au départ de Montpellier (`MPL`) | À ajouter |
| 13–15 | Expressions régulières sur les passeports et numéros de vol ; compagnies possédant plus de deux long-courriers | À ajouter |

Exemple déjà présent dans le rapport — prix moyen des réservations par vol :

```sql
SELECT vol_fk, AVG(prix) AS prix_moyen
FROM t_reservation
GROUP BY vol_fk
ORDER BY prix_moyen ASC;
```

`GROUP BY` regroupe les réservations par vol, `AVG` calcule leur prix moyen et `ORDER BY` classe les moyennes de la plus petite à la plus grande.

## Prochaines étapes

- [ ] Compléter les requêtes 6 à 15 et expliquer les points techniques des 15 requêtes.
- [ ] Justifier les index nécessaires aux deux requêtes du CdC, distinguer les index existants de ceux à créer et fournir le SQL correspondant.
- [ ] Créer les cinq rôles demandés : administrateur, gestionnaire des vols, agent de réservation, agent de comptoir et analyste ; attribuer les privilèges adaptés et créer au moins un utilisateur par rôle.
- [ ] Présenter la transaction d’annulation d’un vol avec ses réservations et expliquer le second cas de transaction fourni dans le CdC.
- [ ] Vérifier la cohérence entre l’analyse des jours de semaine, le modèle final et les tables effectivement créées.
- [ ] Compléter la section sur l’utilisation de l’IA et rédiger la conclusion du rapport.
- [ ] Regrouper les requêtes finalisées dans des scripts `.sql` faciles à réexécuter et ajouter des aperçus du MCD/MLD pour leur lecture sur GitHub.

## Auteur et documentation

**Romain Augusto** — étudiant développeur à l’ETML  
**Chef de projet :** Grégory Charmier  
**Période :** du 24.08.2026 au 28.10.2026

- [Dépôt GitHub](https://github.com/Pt74bsx/P_DB_GestionAeroport)
- [Profil GitHub](https://github.com/Pt74bsx)
- Cahier des charges : `DOC/E-P_DB-GCR001-CdC-2026.pdf`
- Rapport Word : dossier `DOC/annexes/`
- Fichier de requêtes : `DOC/annexes/requete.txt`
- Modèle principal : `MCD-MLD/db_aeroport.loo`

Le rapport mentionne l’utilisation de ChatGPT pour comprendre MERISE et rechercher des pistes de résolution lors de l’import des données. Le cahier des charges demande de documenter ces aides de manière détaillée et explicite.
