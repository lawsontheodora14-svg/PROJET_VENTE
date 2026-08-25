# Fidélisation client dans le e-commerce (Analyse par modèle logit/probit)

## Objectif

Ce projet examine les facteurs associés à la fidélisation des clients dans le secteur du e-commerce, à partir de données de transactions réelles issues d'un site de vente en ligne basé au Royaume-Uni (dataset Online Retail, période 2010-2011).

## Question de recherche

Quels facteurs liés au comportement d'achat (montant dépensé, quantité achetée, pays du client) sont associés à la probabilité qu'un client passe plusieurs commandes plutôt qu'une seule ?

## Données

**Source** : [Online Retail Dataset (UCI Machine Learning Repository)](https://archive.ics.uci.edu/dataset/352/online+retail)

**Unité d'observation initiale** : ligne de transaction, agrégée ensuite au niveau client (n ≈ 4 267 après nettoyage)

**Variables clés construites** :
- `fidele` : variable binaire (1 = client ayant commandé plus d'une fois, 0 = client ponctuel) — variable expliquée
- `panier_moyen` : montant moyen dépensé par commande
- `quantite_totale` : quantité totale d'articles achetés
- `pays_simplifie` : pays du client, regroupé sur les 5 principaux pays représentés

## Méthodologie

1. Import, nettoyage des transactions (suppression des commandes annulées, valeurs manquantes, quantités/prix négatifs)
2. Agrégation des données au niveau client
3. Construction de la variable cible de fidélité et des variables explicatives
4. Traitement des valeurs extrêmes (suppression au-delà du 99e percentile) pour permettre l'estimation numérique des modèles
5. Analyse exploratoire (distribution, corrélations)
6. Estimation de deux modèles binaires : logit et probit
7. Lecture des résultats via les effets marginaux
8. Discussion critique et synthèse

## Principaux résultats

| Variable | Effet marginal (logit) | Significativité |
|---|---|---|
| `panier_moyen` | -0,0011 | p < 0,001 |
| `quantite_totale` | +0,0013 | p < 0,001 |
| Pays | Non significatif | p > 0,05 |

Un volume d'achat élevé est associé à une probabilité accrue de fidélité, tandis qu'un panier moyen élevé y est associé négativement une fois le volume pris en compte. Les résultats sont cohérents entre les modèles logit et probit.

## Limites

Les modèles présentent un risque de quasi-séparation (20 à 23% des observations parfaitement prédites), invitant à la prudence sur la magnitude exacte des coefficients. La suppression des outliers limite par ailleurs la généralisation aux gros comptes (probablement B2B). La relation mise en évidence reste associative, non causale.

## Outils utilisés

- Python (pandas, statsmodels, matplotlib)
- Jupyter Notebook

## Auteur

Théodora LAWSON
