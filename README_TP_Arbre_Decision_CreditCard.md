# README - TP Arbre de Decision (Credit Card Fraud Detection)

## 1) Contexte du projet
Ce notebook presente un projet de Machine Learning de classification binaire applique a la detection de fraude bancaire.

Objectif metier :
- Detecter automatiquement si une transaction est frauduleuse (classe 1) ou non frauduleuse (classe 0).
- Reduire les erreurs de classification dans un contexte bancaire, ou les faux negatifs et faux positifs ont un cout eleve.

Notebook source : TP_Arbre_Decision (1).ipynb

---

## 2) Jeu de donnees
Le projet utilise le fichier : creditcard.csv

Caracteristiques principales :
- 284 807 transactions
- Variables numeriques majoritairement issues d'une transformation ACP (V1 a V28)
- Variables supplementaires : Time et Amount
- Variable cible : Class
  - 0 = transaction non frauduleuse
  - 1 = transaction frauduleuse

Point important :
- Le dataset est fortement desequilibre (la fraude est tres minoritaire).

---

## 3) Pipeline de travail realise
Le notebook suit une logique de projet complete, de l'analyse metier jusqu'aux recommandations de deploiement.

### Phase 0 - Installation et imports
Librairies utilisees :
- pandas
- matplotlib
- seaborn
- scikit-learn
- imbalanced-learn (SMOTE)

### Phase 1 - Business Understanding
- Definition de la problematique metier
- Traduction en probleme ML de classification binaire
- Identification des metriques de performance importantes

### Phase 2 - Data Understanding
- Chargement du dataset
- Inspection initiale (dimensions, types, apercu)
- Analyse de la distribution de la variable cible
- Verification des valeurs manquantes
- Statistiques descriptives
- Visualisations comparatives par classe
- Matrice de correlation et variables les plus liees a la cible

### Phase 3 - Data Preparation
- Separation des variables explicatives X et de la cible y
- Split train/test avec stratification (80/20)
- Gestion du desequilibre avec SMOTE

### Phase 4 - Modeling
Trois modeles d'arbre de decision ont ete entraines :
- Modele 1 : critere Gini, max_depth = 3
- Modele 2 : critere Entropy, max_depth = 3
- Modele 3 : critere Gini, sans limite de profondeur

### Phase 5 - Evaluation
- Comparaison des accuracies train/test des 3 modeles
- Analyse du surapprentissage
- Classification report du modele retenu
- Matrice de confusion
- Courbe ROC + score AUC
- Visualisation de l'arbre
- Importance des variables

### Phase 6 - Conclusions et recommandations
- Synthese des performances
- Limites identifiees
- Pistes d'amelioration
- Suggestions de deploiement en contexte metier

---

## 4) Resultats cles observes dans le notebook
D'apres la synthese renseignee dans le notebook :
- Accuracy globale : environ 97%
- Recall classe fraude : environ 95%
- Recall classe non fraude : environ 98%
- AUC-ROC : environ 0.98
- Variable importante souvent citee : V14

Interpretation :
- Les resultats sont globalement tres bons pour une premiere version.
- Le modele avec profondeur contrainte generalise mieux que l'arbre non contraint (limitation du surapprentissage).

---

## 5) Lecture metier des erreurs
En detection de fraude :
- Faux negatif = fraude non detectee (risque financier direct)
- Faux positif = transaction legitime bloquee (impact experience client)

Le projet montre l'importance de ne pas se limiter a l'accuracy et de suivre aussi recall, precision, F1 et AUC.

---

## 6) Limites et bonnes pratiques
Points de vigilance identifies :
- Le desequilibre de classes reste un enjeu central.
- Les variables d'origine ne sont pas accessibles (confidentialite + ACP), ce qui limite l'interpretabilite metier.
- Pour une evaluation rigoureuse, le reequilibrage SMOTE doit etre applique uniquement sur les donnees d'entrainement (et non sur le jeu de test).

---

## 7) Pistes d'amelioration
Ameliorations recommandees :
- Optimisation d'hyperparametres (GridSearchCV / RandomizedSearchCV)
- Validation croisee stratifiee
- Test d'autres algorithmes (Random Forest, XGBoost, etc.)
- Calibration du seuil de decision selon le cout metier
- Suivi en production (drift, performance, re-entrainement periodique)

---

## 8) Mini guide d'execution
1. Ouvrir le notebook TP_Arbre_Decision (1).ipynb.
2. Verifier que creditcard.csv est present dans le meme dossier.
3. Installer les dependances si necessaire :
   - pandas, matplotlib, seaborn, scikit-learn, imbalanced-learn
4. Executer les cellules dans l'ordre.
5. Analyser les metriques finales et la matrice de confusion avant toute decision metier.

---

## 9) Livrables du dossier
- Notebook principal : TP_Arbre_Decision (1).ipynb
- Dataset : creditcard.csv
- Documentation (ce fichier) : README_TP_Arbre_Decision_CreditCard.md

Ce README sert de resume operationnel et de mini documentation pour comprendre rapidement le travail realise et reutiliser la demarche sur un projet similaire.
