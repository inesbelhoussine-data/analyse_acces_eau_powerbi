# 🌍 Analyse de l'accès à l'eau potable dans le monde

## 📌 Présentation du projet

Ce projet a été réalisé dans le cadre de ma formation **Data Analyst**.

L'objectif est d'accompagner **DWFA (Drinking Water For All)**, une ONG spécialisée dans l'accès à l'eau potable, dans l'analyse des besoins en eau à l'échelle mondiale.

À partir de plusieurs jeux de données démographiques, sanitaires, politiques et liés à l'accès à l'eau, j'ai conçu un **tableau de bord interactif avec Power BI** permettant d'explorer la situation selon trois niveaux géographiques :

- 🌍 Monde
- 🗺️ Région
- 🇺🇳 Pays

---

## 🎯 Objectifs

Le tableau de bord doit permettre d'identifier les zones dans lesquelles les actions de l'ONG pourraient être pertinentes.

Trois domaines d'intervention sont étudiés :

### 1. Création de nouveaux services d'accès à l'eau

Analyse de la relation entre :

- la population urbaine ;
- l'accès aux services d'eau potable de base.

### 2. Modernisation des services existants

Analyse de la relation entre :

- l'accès aux services d'eau potable de base ;
- l'accès à des services d'eau potable gérés en toute sécurité.

### 3. Accompagnement institutionnel

Analyse croisée de :

- la stabilité politique ;
- l'efficacité liée aux politiques d'accès à l'eau.

Un filtre quantitatif de **stabilité politique** permet également d'adapter l'analyse en fonction du niveau de stabilité des pays.

---

# 📊 Tableau de bord

Le rapport Power BI est organisé en **trois pages complémentaires**.

## 🌍 Vue mondiale

Cette page fournit une vision globale de la situation de l'accès à l'eau.

Elle présente notamment :

- la population totale ;
- le taux d'accès à l'eau potable de base ;
- le taux d'accès à l'eau gérée en toute sécurité ;
- les décès liés aux problématiques WASH ;
- la répartition de la population urbaine et rurale ;
- les différences entre régions ;
- la stabilité politique.

Des filtres permettent d'affiner l'analyse selon l'année, le pays et la stabilité politique.

---

## 🗺️ Vue régionale

Cette page permet d'étudier plus précisément une région et les pays qui la composent.

Elle permet notamment d'analyser :

- la population ;
- l'accès à l'eau potable ;
- l'accès à une eau gérée en toute sécurité ;
- la mortalité liée aux problématiques WASH ;
- les différences entre les pays d'une même région.

---

## 🇺🇳 Vue nationale

Cette page permet d'approfondir l'analyse d'un pays sélectionné.

Elle comprend notamment :

- la population totale ;
- la population urbaine et rurale ;
- l'accès à l'eau potable de base ;
- l'accès à une eau gérée en toute sécurité ;
- la mortalité WASH ;
- la stabilité politique ;
- l'évolution démographique ;
- plusieurs analyses de corrélation entre indicateurs.

Les nuages de points permettent notamment d'explorer les trois domaines d'intervention de DWFA.

---

# 🧹 Préparation et nettoyage des données

La préparation des données a été réalisée avec **Power Query**.

Les principales étapes ont consisté à :

- vérifier et corriger les types de données ;
- contrôler les valeurs manquantes ;
- vérifier les années disponibles ;
- gérer les différentes granularités des données ;
- contrôler la cohérence géographique ;
- préparer les variables nécessaires aux analyses ;
- vérifier la cohérence des agrégations.

### 🔎 Contrôle qualité : cas de la Chine

Lors de la vérification des indicateurs agrégés, une redondance a été identifiée entre les séries :

- `China`
- `China, mainland`

Cette redondance provoquait un **double comptage de la population chinoise** et entraînait une surestimation de la population mondiale.

La série `China, mainland` a donc été exclue afin de conserver une seule observation représentative et d'obtenir des agrégations cohérentes.

---

# 🗃️ Modélisation des données

Le modèle Power BI s'appuie sur des dimensions communes permettant de filtrer les différentes tables de données.

### Dimensions principales

- **RegionCountry** : dimension géographique reliant les pays à leurs régions ;
- **DimYear** : dimension temporelle permettant de gérer les années.

La table `RegionCountry` constitue le référentiel géographique utilisé pour propager les filtres de pays et de région vers les différentes tables de faits.

Cette organisation permet d'éviter de dupliquer inutilement les informations géographiques directement dans les tables de données.

---

# 🧮 Mesures DAX

Plusieurs mesures ont été créées afin de rendre les indicateurs dynamiques selon le contexte de filtrage.

Parmi les principales mesures :

- Population totale
- Population urbaine
- Population rurale
- Taux de population urbaine
- Accès à l'eau potable de base
- Accès à l'eau gérée en toute sécurité
- Décès WASH
- Taux de mortalité WASH
- Stabilité politique
- Efficacité politique de l'eau

### 💧 Indicateur d'efficacité politique de l'eau

Un indicateur analytique a été construit afin de combiner :

- un niveau élevé d'accès à l'eau potable ;
- un niveau faible de mortalité liée aux problématiques WASH.

Le taux de mortalité WASH est normalisé avec une **normalisation Min-Max**, puis inversé afin qu'une mortalité faible contribue positivement au score.

Principe de calcul :

`Efficacité politique eau = (Accès eau + (1 - Mortalité normalisée)) / 2`

Cet indicateur a été créé spécifiquement pour les besoins de cette analyse et ne constitue pas un indice officiel externe.

---

# 📈 Choix des visualisations

Les visualisations ont été sélectionnées selon la nature de l'information à transmettre :

- **Cartes KPI** → indicateurs principaux ;
- **Graphiques en courbes** → évolutions temporelles ;
- **Diagrammes en barres** → comparaisons entre pays ou régions ;
- **Barres empilées à 100 %** → comparaison de proportions ;
- **Nuages de points** → analyse des relations entre variables quantitatives ;
- **Cartes géographiques** → visualisation des disparités territoriales.

L'objectif était de conserver un tableau de bord **lisible, cohérent et facilement interprétable**.

---

# ♿ Accessibilité et ergonomie

Une attention particulière a été portée à :

- la hiérarchie visuelle ;
- la lisibilité des titres et indicateurs ;
- la cohérence des couleurs ;
- le contraste ;
- la disposition des filtres ;
- la cohérence entre les différentes pages ;
- la limitation de la surcharge visuelle.

---

# ⚠️ Limites des données

Les données relatives à la mortalité WASH sont disponibles uniquement pour **l'année 2016** dans le jeu de données utilisé.

Les indicateurs WASH ne peuvent donc pas être analysés comme une série temporelle sur l'ensemble de la période.

Les valeurs absentes pour les autres années sont volontairement laissées vides afin de ne pas les remplacer artificiellement par zéro.

---

# 🛠️ Compétences mobilisées

### Power BI
- Création de tableaux de bord
- Data visualisation
- Filtres et interactions
- Conception d'indicateurs

### Power Query
- Nettoyage des données
- Transformation des données
- Contrôle qualité

### DAX
- Création de mesures
- Gestion du contexte de filtre
- KPI dynamiques
- Normalisation Min-Max

### Modélisation
- Tables de dimensions
- Relations entre tables
- Modélisation géographique et temporelle

---


# 👩‍💻 À propos

**Ines Belhoussine**

Data Analyst

`Power BI` • `DAX` • `Power Query` • `SQL` • `Python` • `Data Visualisation` • `Modélisation de données`
