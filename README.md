# 📘 Gestion de Prêts et Remboursements  
**Documentation Technique – Version 1.0**

Système complet de gestion des prêts clients, suivi des remboursements, calcul des encours et génération de rapports.

---

## 📑 Table des Matières
1. [Contexte](#contexte)  
2. [Problématique](#problématique)  
3. [Objectifs](#objectifs)  
4. [Structure de la Base de Données](#structure-de-la-base-de-données)  
5. [Fonctionnalités Principales](#fonctionnalités-principales)  
6. [Technologies Utilisées](#technologies-utilisées)  
7. [Diagrammes](#diagrammes)  
8. [Tutoriel Vidéo](#tutoriel-vidéo)

---

## 1️⃣ Contexte
Dans le secteur bancaire et financier, la gestion des prêts nécessite une solution numérique fiable capable de suivre les remboursements, d’éviter les erreurs et d’améliorer l’analyse des données.

---

## 2️⃣ Problématique
La gestion manuelle entraîne :

- erreurs de calcul  
- retard dans les mises à jour  
- difficulté à produire des rapports fiables  
- manque de visibilité sur l'état des prêts  

---

## 3️⃣ Objectifs

- **Centraliser les données** (clients, prêts, paiements)  
- **Automatiser les calculs** (intérêts, mensualités, encours)  
- **Faciliter le suivi** des prêts et retards  
- **Générer des rapports** statistiques  

---

## 4️⃣ Structure de la Base de Données

### 📌 Tables principales

| Table          | Description                | Champs principaux                                   |
|----------------|----------------------------|-----------------------------------------------------|
| **Client**     | Informations clients       | id, nom, catégorie, ville                           |
| **Pret**       | Informations sur les prêts | id, client_id, montant, taux, date_debut, durée     |
| **Remboursement** | Historique des paiements | id, pret_id, date, montant, type                    |
| **Utilisateur**   | Authentification système | login, password, role                               |

---

### 📄 Script SQL

```sql
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
