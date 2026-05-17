# Système de Guidage Latéral de Véhicule sous MATLAB/Simulink

## Présentation du Projet

Ce projet présente la conception, la modélisation et la validation d’un système de guidage latéral de véhicule développé selon une approche Model Based Design (MBD) sous MATLAB/Simulink.

L’objectif principal est d’assurer le suivi d’une trajectoire sinueuse tout en minimisant l’erreur latérale à l’aide d’un contrôleur PID et d’une supervision sous Stateflow.

Le système développé intègre :

- un modèle dynamique de véhicule 2D,
- la génération de trajectoires de référence,
- un contrôleur PID de guidage latéral,
- une logique de supervision Stateflow,
- des validations MIL, SIL et PIL,
- des outils de visualisation 2D et 3D.

---

# Objectifs du Projet

Les principaux objectifs du projet sont :

- modéliser la dynamique latérale d’un véhicule,
- concevoir une architecture de contrôle sous Simulink,
- assurer le suivi d’une trajectoire complexe,
- minimiser l’erreur de trajectoire,
- valider le comportement du système via les approches MIL, SIL et PIL,
- analyser le comportement du véhicule à travers des simulations 2D et 3D.

---

# Description Générale du Système

L’architecture globale du système repose sur une structure de contrôle en boucle fermée composée de plusieurs sous-systèmes.

Le système comprend principalement :

- un bloc Environment pour la génération de trajectoire,
- un bloc Controller pour le calcul de la commande,
- un bloc Plant représentant le modèle dynamique du véhicule,
- un bloc Stateflow pour la supervision,
- des blocs de visualisation et d’analyse.

Le contrôleur calcule en temps réel l’angle de braquage nécessaire afin de réduire l’erreur entre la trajectoire réelle et la trajectoire de référence.

---

# Modèle Dynamique du Véhicule

Le véhicule est modélisé à l’aide d’un modèle cinématique bicyclette 2D simplifié.

Les équations dynamiques utilisées sont les suivantes :

<p align="center">

$ẋ = v \cos(\psi)$

</p>

<p align="center">

$ẏ = v \sin(\psi)$

</p>

<p align="center">

$\dot{\psi} = \frac{v}{L}\tan(\delta)$

</p>

Avec :

| Variable | Description |
|---|---|
| $x$ | Position longitudinale du véhicule |
| $y$ | Position latérale du véhicule |
| $\psi$ | Angle d’orientation du véhicule |
| $\delta$ | Angle de braquage |
| $v$ | Vitesse longitudinale du véhicule |
| $L$ | Empattement du véhicule |

Les hypothèses simplificatrices adoptées sont :

- vitesse longitudinale constante,
- mouvement plan du véhicule,
- dynamique cinématique simplifiée,
- braquage direct des roues avant.

---

# Architecture Simulink

L’architecture Simulink est organisée sous forme de sous-systèmes afin de garantir une structure claire et modulaire.

## Architecture Globale

*Insérer ici une image de l’architecture globale Simulink.*

Les principaux sous-systèmes sont :

### Environment

Ce sous-système permet :

- la génération de trajectoires de référence,
- la sélection des scénarios,
- l’introduction des perturbations.

### Controller

Le contrôleur assure :

- le calcul de l’erreur latérale,
- le calcul de l’erreur d’orientation,
- la génération de la commande de braquage via un PID.

### Plant

Le bloc Plant implémente :

- le modèle dynamique du véhicule,
- les équations cinématiques,
- les intégrateurs d’état.

### Supervision

Le système de supervision est développé sous Stateflow afin de gérer les différents modes de fonctionnement.

### Visualization

Les blocs de visualisation permettent :

- l’affichage des trajectoires,
- l’analyse des signaux,
- la simulation 3D du véhicule.

---

# Génération de Trajectoire

La trajectoire de référence est générée à partir d’une combinaison de fonctions sinusoïdales afin d’obtenir une route complexe et sinueuse.

La trajectoire utilisée est définie par :

<p align="center">

$y_{ref}(x)=A_1\sin(B_1x)+A_2\sin(B_2x)+A_3\sin(B_3x)$

</p>

Cette approche permet :

- de générer des trajectoires variées,
- de simuler des routes complexes,
- d’évaluer le comportement du système dans plusieurs conditions.

## Bloc de Génération de Trajectoire

*Insérer ici une image du bloc Environment.*

---

# Conception du Contrôleur PID

Le système utilise un contrôleur PID afin de corriger l’erreur de trajectoire.

Le contrôleur agit à partir :

- de l’erreur latérale,
- de l’erreur d’orientation.

Le PID génère la commande de braquage envoyée au modèle du véhicule.

## Contrôleur PID sous Simulink

*Insérer ici une image du contrôleur PID.*

Les paramètres du PID sont ajustés à l’aide du Simulink PID Tuner afin d’obtenir :

- une bonne précision de suivi,
- une stabilité correcte,
- un temps de réponse satisfaisant.

## Réglage du PID

*Insérer ici une image du PID Tuner.*

---

# Supervision Stateflow

La supervision du système est réalisée à l’aide d’une machine à états développée sous Stateflow.

Les états implémentés sont :

- Init,
- Standby,
- Nominal,
- Emergency.

Les transitions dépendent :

- de l’activation du système,
- de la présence de défauts,
- des seuils d’erreur.

## Machine à États Stateflow

*Insérer ici une image du diagramme Stateflow.*

---

# Validation MIL

La première phase de validation est réalisée via une approche Model In the Loop (MIL).

L’ensemble du système est simulé directement sous Simulink afin d’évaluer :

- le suivi de trajectoire,
- la stabilité du véhicule,
- les performances du contrôleur.

## Simulation MIL

*Insérer ici une image de simulation MIL.*

Les résultats obtenus montrent :

- une bonne précision de suivi,
- une stabilité satisfaisante,
- une réduction importante de l’erreur latérale.

---

# Validation SIL

La validation Software In the Loop (SIL) permet de vérifier la cohérence entre :

- le modèle Simulink,
- le code généré automatiquement.

Le contrôleur généré est exécuté dans un environnement logiciel afin de comparer les résultats avec ceux du modèle original.

## Validation SIL

*Insérer ici une image SIL.*

Les résultats montrent une forte correspondance entre les sorties MIL et SIL.

---

# Validation PIL

La validation Processor In the Loop (PIL) consiste à exécuter le code généré sur une cible embarquée.

Dans ce projet, le contrôleur est exécuté sur une carte Arduino tout en conservant l’environnement de simulation sous Simulink.

## Validation PIL

*Insérer ici une image PIL.*

Cette étape permet de valider :

- l’exécution embarquée,
- le comportement temps réel,
- la cohérence avec les simulations précédentes.

---

# Visualisation 2D et 3D

Le projet intègre des outils de visualisation permettant d’analyser le comportement du système.

Les visualisations comprennent :

- un affichage XY Graph,
- des scopes de signaux,
- une représentation 2D du véhicule,
- une simulation 3D du déplacement.

## Visualisation 2D

*Insérer ici une image de trajectoire 2D.*

## Simulation 3D

*Insérer ici une image de simulation 3D.*

La visualisation 3D permet d’observer :

- le déplacement du véhicule,
- le suivi de trajectoire,
- le comportement dynamique global.

---

# Outils et Technologies

Le projet a été développé à l’aide des outils suivants :

- MATLAB
- Simulink
- Stateflow
- Simulink Dashboard
- PID Tuner
- Simulink 3D Animation
- Embedded Coder
- Arduino

---

# Méthodologie de Validation

Le projet suit une démarche progressive de validation MBD :

1. Modélisation du système
2. Simulation sous Simulink
3. Validation MIL
4. Validation SIL
5. Validation PIL
6. Analyse et visualisation des résultats

---

# Auteur

Yasmine Sbai

Étudiante en Systèmes Embarqués et Intelligence Artificielle

INSEA – Maroc

---

# Encadrant

M. Anass Mansouri

---

# Contexte Académique

Projet de Model Based Design (MBD)

Année Universitaire : 2024/2025
