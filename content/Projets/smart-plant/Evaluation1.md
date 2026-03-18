+++
draft = "true"
+++

# TP 1

## Objectif

L’objectif de ce travail pratique est de concevoir et programmer un **système autonome de surveillance et d’arrosage d’une plante** à l’aide d’une carte Arduino, de capteurs et d’actionneurs.

L’étudiant devra réaliser **le circuit électronique complet** ainsi que **le programme Arduino** permettant d’assurer le fonctionnement global du système.

---

## Matériel utilisé

* Carte Arduino
* Capteur de température et d’humidité ambiante
* Capteur d’humidité du sol
* Pompe à eau
* Transistor + diode de protection
* LED rouge
* LED bleue
* Résistances
* Breadboard et fils de connexion

---

## Description du système à réaliser

Le système doit permettre :

### 1. Acquisition des données

Le programme doit :

* mesurer la **température ambiante**
* mesurer l’**humidité ambiante**
* mesurer l’**humidité du sol**

Les capteurs doivent être lus régulièrement et le programme doit calculer :

👉 **la moyenne des valeurs toutes les 30 secondes**

---

### 2. Indication visuelle (LED)

* La **LED rouge doit clignoter** si la température moyenne dépasse **30 °C**
* La **LED bleue doit clignoter** si l’humidité moyenne du sol est **inférieure à 40 %**

La fréquence de clignotement est laissée au choix de l’étudiant.

---

### 3. Gestion intelligente de l’arrosage

La pompe doit fonctionner selon la logique suivante :

* La pompe démarre si **l’humidité du sol est inférieure à 35 %**
* Une fois démarrée, la pompe peut fonctionner **au maximum pendant 5 secondes**
* Après un cycle d’arrosage, le système doit attendre **1 minute avant de prendre une nouvelle décision**
* La pompe s’arrête définitivement seulement si **l’humidité du sol dépasse 55 %**

---

### 4. Affichage sur le moniteur série

Toutes les **30 secondes**, le programme doit afficher :

```
Temp avg: XX C
Air humidity avg: XX %
Soil humidity avg: XX %
Pump state: ON / OFF
```

L’affichage doit être clair, structuré et lisible.

---

## Contraintes importantes

* Le circuit doit être **réalisé proprement et de manière sécuritaire**
* La pompe doit être commandée **à l’aide d’un transistor**
* Une **diode de protection** doit être installée
* Le programme doit être **stable et autonome**
* Le système doit fonctionner **sans intervention humaine**

---

## Livrables demandés

1. Circuit fonctionnel démontré en laboratoire
2. Code Arduino démontré en laboratoire
3. Explication orale du fonctionnement du système

---

## Critères d’évaluation

* Fonctionnement correct du système et respect des consignes : 10%
* Qualité du montage électronique : 30%
* Logique de programmation et lisibilité du code : 50%
* Compréhension du fonctionnement : 10%

---
