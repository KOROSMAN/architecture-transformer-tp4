# Architecture Transformer — TP4

Du RNN au Transformer : prédiction de séries temporelles, puis modèles de langage
de type GPT (génération) et BERT (mot masqué), implémentés avec PyTorch.

## Progression
### Partie 1 : du RNN au Transformer
- [x] Étape 0 : Initialisation du projet
- [x] Étape 1 : RNN (sin(x), séquences de 10 valeurs)
- [x] Étape 2 : LSTM
- [x] Étape 3 : Transformer
- [x] Étape 4 : GPT-2 (prédire la suite d'un texte)
- [x] Étape 5 : BERT (prédire un mot masqué)

### Partie 2 : exercices
- [x] Exercice 1 : EnergyTransformer (consommation électrique)
- [x] Exercice 2 : mini-GPT (génération caractère par caractère)
- [x] Exercice 3 : mini-BERT (mots masqués)

## Notebooks
| Notebook | Contenu |
|---|---|
| `01_rnn.ipynb` | RNN : 10 valeurs de sin(x) → valeur suivante |
| `02_lstm.ipynb` | Même tâche avec un LSTM (états h et c, portes) |
| `03_transformer.ipynb` | Mini-Transformer encodeur + comparatif des 3 modèles |
| `04_gpt.ipynb` | GPT-2 préentraîné : prédiction du token suivant, génération |
| `05_bert.ipynb` | BERT multilingue : « Rabat est la [MASK] du Maroc. » |
| `06_ex1_energie.ipynb` | EnergyTransformer : 24 h de consommation → heure suivante |
| `07_ex2_mini_gpt.ipynb` | Mini-GPT entraîné de zéro, masque causal, températures |
| `08_ex3_mini_bert.ipynb` | Mini-BERT entraîné de zéro, masquage 15 % (80/10/10) |

## Résultats
### Série sin(x)
Les trois modèles (RNN, LSTM, Transformer) prédisent correctement la valeur suivante.
Le comparatif détaillé se trouve dans `03_transformer.ipynb`.

### Exercice 1 : consommation électrique (test, en kW)
| Modèle | MAE | RMSE |
|---|---|---|
| **EnergyTransformer** | **0.341** | **0.498** |
| Persistance (h-1) | 0.389 | 0.588 |
| Journalière (h-24) | 0.513 | 0.764 |

Le Transformer réduit l'erreur d'environ 12 % par rapport à la persistance
et de 34 % par rapport à la référence journalière.

### Exercice 2 : mini-GPT
Génération de 200 caractères comparée à des températures de 0.5, 1.0 et 1.5.
Le masque causal est vérifié : modifier un caractère futur ne change pas les prédictions passées.

### Exercice 3 : mini-BERT
Le modèle retrouve les mots masqués à partir du contexte gauche et droit
(exactitude détaillée dans `08_ex3_mini_bert.ipynb`).
Le masque de padding est vérifié : modifier les tokens [PAD] ne change pas les prédictions.

## Ce qu'il faut retenir
| | RNN / LSTM | Transformer |
|---|---|---|
| Lecture | élément par élément, avec une mémoire | toute la séquence en parallèle |
| Ordre des éléments | implicite (lecture séquentielle) | ajouté par l'encodage de position |
| Longues dépendances | difficile (RNN), mieux (LSTM) | direct grâce à l'attention |

| | GPT (décodeur) | BERT (encodeur) |
|---|---|---|
| Attention | causale (gauche → droite) | bidirectionnelle |
| Entraînement | prédire le token suivant | retrouver des tokens masqués |
| Usage | générer du texte | comprendre / classer du texte |

## Données
- **Exercice 1** : le dataset *Individual Household Electric Power Consumption* (UCI)
  n'est pas versionné, car il pèse 127 Mo (au-delà de la limite de 100 Mo de GitHub).
  Le télécharger sur https://archive.ics.uci.edu/dataset/235 et placer
  `household_power_consumption.txt` dans `data/`.
- **Exercice 2** : `data/corpus.txt` est créé par la première cellule du notebook 07
  à partir des explications du notebook de cours (`data/architecture_transformer.ipynb`,
  non versionné).
- **Exercice 3** : le corpus de phrases est généré directement dans le notebook 08.

## Installation et exécution
    uv sync

Puis exécuter les notebooks dans l'ordre, avec le kernel `.venv`.
Les modèles GPT-2 et BERT se téléchargent au premier lancement (~500 Mo et ~700 Mo).