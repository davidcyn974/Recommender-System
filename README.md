# Project Assignment: Movie Pairing Recommender SystemProject Assignment: Movie Pairing Recommender System

## Introduction

Ce projet vise à développer un système de recommandation de films pour un couple d'utilisateur.\
L'objectif est de suggérer des films qui pourraient plaire aux deux membres du couple en se basant sur leurs préférences individuelles.

## Méthodologie

### 1. Collecte et Prétraitement des Données

- Utilisation des datasets MovieLens et IMDb.
<ins>Attention</ins> les datasets name_basics & title_basics d'IMDB n'ont pas été push sur GitHub car trop volumineux.\
Si vous voulez tester mon code, il faudra les télécharger sur le site d'IMDB: 
      - [name_basics](https://datasets.imdbws.com/name.basics.tsv.gz)
      - [title_basics](https://datasets.imdbws.com/title.basics.tsv.gz)
- Fusion des datasets pour inclure les notes, genres et métadonnées des films.
- Nettoyage des données :
    - Suppression des caractères spéciaux
    - Suppression des valeurs manquantes
    - Uniquement les films sont gardés (par exemple pas de séries TV, ni de shorts)
    - Uniformisation des genres
    - Uniformisation des titres
- Filtrage pour ne garder que les films présents dans les deux datasets.

### 2. Ingénierie des Caractéristiques
- Combinaison des données des utilisateurs pour obtenir un profil de couple en faisant la moyenne des notes.
- Sélection des caractéristiques pertinentes : ID du film, titre, année, durée, genres.

- Création d'une matrice d'interaction user-item.
    - Les lignes représentent les utilisateurs.
    - Les colonnes représentent les films.
    - Les valeurs à la position (i,j) dans la matrice représentent les notes données par les utilisateurs aux films (ratings).

### 3. Développement du Modèle

- Implémentation de l'algorithme ALS (Alternating Least Squares)
- Choix des hyperparamètres :
  - Nombre de facteurs latents : 50
  - Nombre d'itérations : 50
  - Régularisation : 0.01

### 4. Algorithme de Recommandation

- Calcul d'un vecteur combiné pour le couple en faisant la moyenne des vecteurs individuels.
- Sélection des n=5, ou n=10 (dans les faits on peut faire varier n), meilleurs films avec les meilleures prédictions de notes.

## Expériences

1. **Préparation des Données** :
   - Division des données en ensembles d'entraînement (80%) et de test (20%).

2. **Entraînement du Modèle** :
   - Entraînement du modèle Alternating Least Squares (ALS) sur l'ensemble d'entraînement.

3. **Génération de Recommandations** :
   - Test du système avec différents couples d'utilisateurs.
   - D'abord les users 1 et 2, puis les users qui ont le plus noté de films et enfin de manière aléatoire pour 10 couples.

## Résultats

- Le modèle ALS a convergé avec une MSE (Mean Squared Error) finale d'environ 0.14.
- Exemple de recommandations pour le couple (utilisateur 1, utilisateur 2) :
```python
user1_id = 1
user2_id = 2

recommendations = recommend_movies_als(user1_id, user2_id, als_model, user_mapping, item_mapping, distinct_movies, num_recommendations=10)

print(recommendations)
```