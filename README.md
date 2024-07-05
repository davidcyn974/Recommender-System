# Project Assignment: Movie Pairing Recommender SystemProject Assignment: Movie Pairing Recommender System

## Introduction

Ce projet vise à développer un système de recommandation de films pour un couple d'utilisateur.\
L'objectif est de suggérer des films qui pourraient plaire aux deux membres du couple en se basant sur leurs préférences individuelles.

## Méthodologie

### 1. Collecte et Prétraitement des Données

- Utilisation des datasets MovieLens et IMDb.
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

- Implémentation de l'algorithme FunkSVD (Singular Value Decomposition).
- Choix des hyperparamètres :
  - Nombre de facteurs latents : 20
  - Nombre d'époques : 50
  - Taux d'apprentissage : 0.005
  - Régularisation : 0.02

### 4. Algorithme de Recommandation

- Calcul d'un vecteur combiné pour le couple en faisant la moyenne des vecteurs individuels.
- Sélection des 5 meilleurs films avec les meilleures prédictions de notes.

## Expériences

1. **Préparation des Données** :
   - Division des données en ensembles d'entraînement (80%) et de test (20%).

2. **Entraînement du Modèle** :
   - Entraînement du modèle FunkSVD sur l'ensemble d'entraînement.

3. **Génération de Recommandations** :
   - Test du système avec différents couples d'utilisateurs.

## Résultats

- Le modèle FunkSVD a convergé avec une MSE (Mean Squared Error) finale de [insérer la valeur finale de MSE].
- Exemple de recommandations pour le couple (utilisateur 1, utilisateur 2) :