# Système de Guidage Latéral de Véhicule sous MATLAB/Simulink

## Présentation Générale

Ce projet présente la conception, la modélisation et la validation d’un système de guidage latéral de véhicule développé selon une approche Model-Based Design (MBD) sous MATLAB/Simulink.

L’objectif principal est d’assurer le suivi automatique d’une trajectoire sinueuse tout en minimisant l’erreur latérale à l’aide d’un contrôleur PID associé à une supervision sous Stateflow.

Le système développé repose sur :

- une modélisation dynamique simplifiée du véhicule,
- une génération de route sinueuse,
- un calcul des erreurs de trajectoire,
- une commande PID,
- une supervision Stateflow,
- une validation MIL / SIL / PIL,
- une visualisation 2D et 3D.

---

# Analyse et Modélisation du Système

L’architecture du système a été conçue selon une approche hiérarchique séparant clairement :

- l’environnement,
- le contrôleur,
- le plant,
- les capteurs,
- la supervision.

Une modélisation SysML a été utilisée afin de structurer les exigences, les interactions et l’architecture globale du système.

Les principaux éléments modélisés sous SysML sont :

- diagrammes des exigences,
- diagrammes de cas d’utilisation,
- diagrammes de blocs,
- diagrammes internes de blocs,
- architecture fonctionnelle du système.

Cette étape permet d’assurer une cohérence entre les besoins fonctionnels et l’implémentation sous Simulink.

---

# Architecture Simulink du Système

L’architecture globale du modèle Simulink est organisée autour des sous-systèmes suivants :

- Environment
- Error Computation
- Controller
- Actuator
- Plant
- Sensors
- Stateflow Supervision
- Visualisation 2D/3D

Le modèle principal respecte une architecture claire séparant :

- la partie commande,
- la partie dynamique véhicule,
- la supervision,
- les scénarios de test.

<p align="center">
  <img src="images/architecture.png" width="950">
</p>

<p align="center">
Architecture globale du système sous Simulink.
</p>

---

# Modèle Dynamique du Véhicule

Le véhicule est représenté par un modèle cinématique bicyclette simplifié 2D.

Ce modèle permet de représenter le déplacement longitudinal, latéral ainsi que l’orientation du véhicule à l’aide d’équations simples compatibles avec une approche pédagogique MBD.

Les équations utilisées sont :

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
| ψ | Orientation du véhicule |
| δ | Angle de braquage |
| v | Vitesse longitudinale |
| L | Empattement |
| dy_pert | Perturbation latérale |

---

# Hypothèses Simplificatrices

Le modèle adopté repose sur plusieurs hypothèses simplificatrices :

- vitesse longitudinale constante,
- mouvement plan 2D,
- faibles angles de braquage,
- absence de dynamique complexe des pneus,
- absence de transfert de charge,
- véhicule représenté par un modèle bicyclette simplifié.

Ces hypothèses permettent d’obtenir un modèle simple, stable et facilement exploitable sous Simulink.

---

# Génération de la Route de Référence

La trajectoire de référence est générée à partir d’une combinaison de fonctions sinusoïdales afin d’obtenir une route sinueuse complexe.

La trajectoire utilisée est définie par :

<p align="center">

y_ref(x) = A1 sin(B1 x) + A2 sin(B2 x) + A3 sin(B3 x)

</p>

Cette approche permet :

- une variation progressive de la courbure,
- plusieurs changements de direction,
- une meilleure validation du contrôleur.

---

# Contrôleur PID

Le guidage latéral du véhicule est assuré par un contrôleur PID.

Le rôle du contrôleur est de calculer l’angle de braquage nécessaire afin de réduire :

- l’erreur latérale,
- l’erreur d’orientation.

Le contrôleur agit continuellement sur le véhicule afin d’assurer le suivi de la trajectoire de référence.

<p align="center">
  <img src="images/pid_controller.png" width="750">
</p>

<p align="center">
Implémentation du contrôleur PID sous Simulink.
</p>

---

# Supervision Stateflow

La supervision du système est réalisée à l’aide d’une machine à états Stateflow.

La logique de supervision permet :

- l’initialisation du système,
- le passage en mode opérationnel,
- la détection des défauts,
- l’activation du mode sécurité.

Les états principaux implémentés sont :

- Init
- Standby
- Nominal
- Emergency

<p align="center">
  <img src="images/stateflow.png" width="700">
</p>

<p align="center">
Machine à états Stateflow du système.
</p>

---

# Validation MIL / SIL / PIL

Le projet intègre plusieurs niveaux de validation conformément à une démarche Model-Based Design.

## MIL — Model In The Loop

Validation fonctionnelle complète du modèle Simulink.

Cette étape permet de vérifier :

- le comportement dynamique,
- le suivi de trajectoire,
- les performances du contrôleur.

---

## SIL — Software In The Loop

Validation du code généré automatiquement à partir du modèle Simulink.

Cette étape permet de comparer :

- le comportement du modèle,
- le comportement du code généré.

---

## PIL — Processor In The Loop

Validation du contrôleur compilé sur une cible processeur.

Cette étape permet :

- l’analyse du temps d’exécution,
- la vérification du comportement embarqué,
- la validation de la compatibilité temps réel.

---

# Simulation 2D

Une visualisation 2D est utilisée afin d’observer :

- la trajectoire de référence,
- la trajectoire réelle du véhicule,
- l’évolution de l’erreur latérale.

<p align="center">
  <img src="images/trajectory2D.png" width="850">
</p>

<p align="center">
Suivi de trajectoire dans le plan XY.
</p>

---

# Simulation 3D

Une scène 3D est intégrée afin de visualiser le déplacement du véhicule sur une route sinueuse complexe.

La simulation 3D permet :

- une meilleure interprétation du comportement dynamique,
- une visualisation réaliste du guidage latéral,
- une démonstration complète du système.

<p align="center">
  <img src="images/simulation3D.png" width="950">
</p>

<p align="center">
Visualisation 3D du véhicule sous Simulink.
</p>

---

# Résultats Obtenus

Les simulations réalisées montrent :

- un suivi correct de trajectoire,
- une réduction significative de l’erreur latérale,
- une bonne stabilité du véhicule,
- un comportement cohérent dans différents scénarios.

Les différents tests réalisés incluent :

- scénario nominal,
- changement de consigne,
- perturbation latérale,
- défaut simplifié.

---

# Perspectives d’Amélioration

Les principales améliorations possibles sont :

- intégration d’une vitesse variable,
- ajout d’un modèle dynamique plus réaliste,
- prise en compte des effets pneumatiques,
- intégration de capteurs réels,
- validation HIL sur matériel embarqué,
- amélioration de la visualisation 3D,
- intégration d’un environnement routier plus complexe.

---
