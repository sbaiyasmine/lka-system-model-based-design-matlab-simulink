# Système de Guidage Latéral de Véhicule sous MATLAB/Simulink

## Présentation du Projet

Ce projet présente la conception, la modélisation et la validation d’un système de guidage latéral de véhicule développé sous MATLAB/Simulink selon une approche Model-Based Design (MBD).

L’objectif principal est d’assurer le suivi d’une trajectoire sinueuse tout en minimisant l’erreur latérale à l’aide d’un contrôleur PID associé à une supervision sous Stateflow.

Le système développé intègre :

- un modèle dynamique simplifié de véhicule 2D,
- une génération de route sinueuse,
- un contrôleur PID de guidage,
- une supervision par machine à états,
- des simulations MIL, SIL et PIL,
- une visualisation 2D et 3D du comportement du véhicule.

---

## Auteur

Yasmine Sbai

---

# Architecture Globale du Système

Le système global est organisé autour des blocs principaux suivants :

- Environment
- Error Computation
- Controller
- Actuator
- Plant
- Sensors
- Stateflow Supervision
- Visualisation 2D/3D

<p align="center">
  <img src="images/architecture.png" width="950">
</p>

<p align="center">
Architecture générale du système de guidage latéral sous Simulink.
</p>

---

# Modèle Dynamique du Véhicule

Le véhicule est modélisé à l’aide d’un modèle cinématique bicyclette simplifié 2D.

Les équations dynamiques utilisées sont :

<p align="center">

dx/dt = v cos(ψ)

dy/dt = v sin(ψ) + dy_pert

dψ/dt = (v / L) tan(δ)

</p>

avec :

| Variable | Description |
|---|---|
| x | Position longitudinale |
| y | Position latérale |
| ψ | Angle d’orientation du véhicule |
| δ | Angle de braquage |
| v | Vitesse longitudinale |
| L | Empattement du véhicule |
| dy_pert | Perturbation latérale |

---

# Hypothèses Simplificatrices

Le modèle adopté repose sur les hypothèses suivantes :

- vitesse longitudinale constante,
- mouvement plan 2D,
- angles de braquage modérés,
- absence de dynamique complexe des pneus,
- absence de transfert de charge,
- véhicule représenté par un modèle bicyclette simplifié.

Ces hypothèses permettent d’obtenir un modèle simple, stable et adapté à une approche pédagogique MBD.

---

# Génération de la Route de Référence

La trajectoire de référence est générée à partir d’une combinaison de fonctions sinusoïdales afin de produire une route sinueuse complexe.

<p align="center">

y_ref(x) = A1 sin(B1 x) + A2 sin(B2 x) + A3 sin(B3 x)

</p>

Cette approche permet :

- une route réaliste,
- des variations de courbure,
- une bonne validation du contrôleur PID.

---

# Contrôleur PID

Le guidage latéral est assuré par un contrôleur PID agissant sur l’erreur de trajectoire.

Le contrôleur calcule l’angle de braquage nécessaire afin de réduire :

- l’erreur latérale,
- l’erreur d’orientation.

<p align="center">
  <img src="images/pid_controller.png" width="750">
</p>

<p align="center">
Implémentation du contrôleur PID sous Simulink.
</p>

---

# Supervision Stateflow

La supervision du système est réalisée à l’aide d’une machine à états Stateflow.

Les états principaux implémentés sont :

- Init
- Standby
- Nominal
- Emergency

La logique de supervision permet :

- l’initialisation du système,
- l’activation du guidage,
- la gestion des défauts,
- le passage en mode sécurité.

<p align="center">
  <img src="images/stateflow.png" width="700">
</p>

<p align="center">
Machine à états Stateflow du système.
</p>

---

# Simulation 2D

Une visualisation 2D est utilisée afin d’observer :

- la trajectoire de référence,
- la trajectoire réelle du véhicule,
- l’erreur de suivi.

<p align="center">
  <img src="images/trajectory2D.png" width="850">
</p>

<p align="center">
Suivi de trajectoire dans le plan XY.
</p>

---

# Simulation 3D

Une scène 3D est intégrée afin de visualiser le comportement dynamique du véhicule sur une route sinueuse complexe.

<p align="center">
  <img src="images/simulation3D.png" width="950">
</p>

<p align="center">
Visualisation 3D du véhicule sous Simulink.
</p>

---

# Validation MIL / SIL / PIL

Le projet intègre plusieurs niveaux de validation :

## MIL — Model In the Loop

Validation fonctionnelle complète du modèle Simulink.

## SIL — Software In the Loop

Validation du code généré automatiquement à partir du contrôleur.

## PIL — Processor In the Loop

Validation du comportement du contrôleur compilé sur une cible processeur.

---

# Structure du Projet

```text
.
├── README.md
├── images/
├── simulink/
│   ├── MIL/
│   ├── SIL/
│   └── PIL/
