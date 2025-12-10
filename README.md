# 📘 Gestion de Prêts et Remboursements

**Documentation Technique -- Version 1.0**

Système complet de gestion des prêts clients, suivi des remboursements,
calcul des encours et génération de rapports.

------------------------------------------------------------------------

## 📑 Table des Matières

1.  [Contexte](#contexte)\
2.  [Problématique](#problématique)\
3.  [Objectifs](#objectifs)\
4.  [Structure de la Base de Données](#structure-de-la-base-de-données)\
5.  [Fonctionnalités Principales](#fonctionnalités-principales)\
6.  [Technologies Utilisées](#technologies-utilisées)\
7.  [Diagrammes](#diagrammes)\
8.  [Tutoriel Vidéo](#tutoriel-vidéo)

------------------------------------------------------------------------

## Contexte

Dans le secteur bancaire et financier, la gestion des prêts nécessite
une solution numérique fiable capable de suivre les remboursements,
d'éviter les erreurs et d'améliorer l'analyse des données.

------------------------------------------------------------------------

## Problématique

La gestion manuelle entraîne :

-   erreurs de calcul\
-   retard dans les mises à jour\
-   difficulté à produire des rapports fiables\
-   manque de visibilité sur l'état des prêts

------------------------------------------------------------------------

## Objectifs

-   **Centraliser les données** (clients, prêts, paiements)\
-   **Automatiser les calculs** (intérêts, mensualités, encours)\
-   **Faciliter le suivi** des prêts et retards\
-   **Générer des rapports** statistiques

------------------------------------------------------------------------

## Structure de la Base de Données

### 📌 Tables principales

  -------------------------------------------------------------------------------
  Table               Description          Champs principaux
  ------------------- -------------------- --------------------------------------
  **Client**          Informations clients id, nom, catégorie, ville

  **Pret**            Informations sur les id, client_id, montant, taux,
                      prêts                date_debut, durée

  **Remboursement**   Historique des       id, pret_id, date, montant, type
                      paiements            

  **Utilisateur**     Authentification     login, password, role
                      système              
  -------------------------------------------------------------------------------

------------------------------------------------------------------------

### 📄 Script SQL

``` sql
CREATE TABLE Client (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    categorie VARCHAR(50) NOT NULL,
    ville VARCHAR(100) NOT NULL,
    date_inscription DATE DEFAULT CURRENT_DATE
);

CREATE TABLE Pret (
    id INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT NOT NULL,
    montant DECIMAL(15,2) NOT NULL,
    taux DECIMAL(5,2) NOT NULL,
    date_debut DATE NOT NULL,
    duree_mois INT NOT NULL,
    statut ENUM('actif', 'clôturé', 'en retard') DEFAULT 'actif',
    FOREIGN KEY (client_id) REFERENCES Client(id) ON DELETE CASCADE
);

CREATE TABLE Remboursement (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pret_id INT NOT NULL,
    date DATE NOT NULL,
    montant DECIMAL(15,2) NOT NULL,
    type_paiement ENUM('espèces', 'virement', 'chèque') DEFAULT 'virement',
    FOREIGN KEY (pret_id) REFERENCES Pret(id) ON DELETE CASCADE
);

CREATE TABLE Utilisateur (
    login VARCHAR(50) PRIMARY KEY,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin', 'gestionnaire') DEFAULT 'gestionnaire',
    date_creation TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

------------------------------------------------------------------------

## Fonctionnalités principales

### 👤 Gestion des clients

-   CRUD clients\
-   Filtrage par catégorie / ville\
-   Consultation fiche détaillée\
-   Calcul encours par client

### 💰 Gestion des prêts

-   Enregistrement d'un prêt\
-   Calcul automatique des mensualités\
-   Suivi de l'état du prêt\
-   Modification des conditions\
-   Clôture automatique

### 🧾 Gestion des remboursements

-   Enregistrement paiements\
-   Historique complet\
-   Détection retards\
-   Génération de reçus

### 📊 Tableaux de bord

-   Encours total\
-   Statistiques\
-   Prêts non remboursés\
-   Graphiques mensuels

------------------------------------------------------------------------

## Technologies Utilisées

  Technologie          Description
  -------------------- -----------------------------
  ☕ **Java**          Langage principal du projet
  🎨 **Swing**         Interface graphique Desktop
  🗄️ **MySQL**         Base de données
  🔌 **JDBC**          Connexion BD
  📊 **JFreeChart**    Graphiques
  🛠️ **NetBeans**      IDE utilisé
  📐 **MagicDraw**     Diagrammes UML
  🗃️ **phpMyAdmin**    Gestion MySQL
  🏗️ **DAO Pattern**   Architecture
  📦 **Maven**         Gestion de dépendances

------------------------------------------------------------------------

## 🏛 Architecture 3 Tiers

    1. Présentation
       - Swing
       - JFreeChart
       - Contrôleurs UI

    2. Métier
       - Services Java
       - Calculs financiers
       - Validation
       - Transactions

    3. Données
       - MySQL
       - JDBC
       - DAO Pattern

------------------------------------------------------------------------

## Diagrammes

### 📌 Use Case

![Use Case](src\images\use_case.png)

### 📌 Architecture

![Architecture](src\images\archit.png)

------------------------------------------------------------------------

## Tutoriel Vidéo

Vidéo explicative du fonctionnement :

    src\images\tuto.mp4

(Le fichier peut être téléchargé directement depuis GitHub)

------------------------------------------------------------------------

## 📌 Footer

Documentation du système de Gestion de Prêts et Remboursements\
**© 2025 -- Tous droits réservés**
