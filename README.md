# Architecture Transformer — TP4

Du RNN au Transformer : prédiction de séries temporelles, puis modèles de langage
de type GPT (génération) et BERT (mot masqué), implémentés avec PyTorch.

## Progression
### Partie 1 : du RNN au Transformer
- [x] Étape 0 : Initialisation du projet
- [X] Étape 1 : RNN (sin(x), séquences de 10 valeurs)
- [X] Étape 2 : LSTM
- [X] Étape 3 : Transformer
- [X] Étape 4 : GPT-2 (prédire la suite d'un texte)
- [ ] Étape 5 : BERT (prédire un mot masqué)

### Partie 2 : exercices
- [ ] Exercice 1 : EnergyTransformer (consommation électrique)
- [ ] Exercice 2 : mini-GPT (génération caractère par caractère)
- [ ] Exercice 3 : mini-BERT (mots masqués)

## Données
Le dataset *Individual Household Electric Power Consumption* (UCI) n'est pas versionné (127 Mo).
Le télécharger sur https://archive.ics.uci.edu/dataset/235 et placer
`household_power_consumption.txt` dans `data/`.

## Installation
    uv sync