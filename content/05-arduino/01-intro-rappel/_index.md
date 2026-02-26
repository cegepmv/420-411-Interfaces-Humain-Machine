+++
title = "Rappel des notions des objets connectés"
weight = "1"
+++

## 🌐 1. Les objets connectés (IoT)

### 📌 Définition
L’**Internet des objets (IoT)** désigne l’ensemble des objets physiques capables de :
- collecter des données (via des capteurs)
- communiquer ces données (via un réseau)
- agir en fonction de ces données

👉 Exemples :
- montre intelligente
- thermostat connecté
- système d’arrosage automatique

---

### ⚙️ Fonctionnement général

Un système IoT comprend généralement :

1. **Capteurs** → collectent les données  
2. **Microcontrôleur** → traite les données  
3. **Communication** → envoie les données (WiFi, USB, etc.)  
4. **Interface utilisateur** → affiche les données (dashboard)

---

## 🧠 2. Les microcontrôleurs

### 📌 Définition
Un **microcontrôleur** est un petit ordinateur intégré dans un circuit électronique.

Il contient :
- un processeur
- de la mémoire
- des entrées/sorties

👉 Il est conçu pour exécuter **une tâche précise en continu**

---

### 🎯 Rôle
- Lire les capteurs
- Prendre des décisions simples
- Contrôler des composants (LED, moteur, pompe)

---

### 🔍 Types de microcontrôleurs

| Type | Exemple | Particularité |
|------|--------|--------------|
| Basique | Arduino Uno | Facile à utiliser |
| Connecté | ESP32 | WiFi + Bluetooth |
| Industriel | PIC, STM32 | Plus puissant |

---

## 🔌 3. La carte Arduino Uno

### 📌 Présentation
La **Arduino Uno** est une carte électronique basée sur un microcontrôleur.

👉 Elle est très utilisée pour :
- l’apprentissage
- les projets électroniques
- les systèmes embarqués

> Regardez les kits qu'on vous a fourni.

![Carte Arduino](https://ledisrupteurdimensionnel.com/wp-content/uploads/2020/10/placa-arduino-composants.jpg)

---

### 💻 Langage utilisé

L’Arduino est programmé en :
- C / C++ simplifié

Fonctions principales :
- `setup()` → exécutée une seule fois
- `loop()` → exécutée en boucle

---

### 🔧 Les principales parties

#### 🔹 Pins digitales
- valeurs : HIGH / LOW
- utilisées pour :
  - LEDs
  - boutons

---

#### 🔹 Pins analogiques
- lisent des valeurs variables (0 → 1023)
- utilisées pour :
  - capteurs (température, humidité)

---

#### 🔹 Port USB
- sert à :
  - programmer la carte
  - communiquer avec l’ordinateur

---

#### 🔹 Bouton RESET
- redémarre le programme

---

#### 🔹 Alimentation
- via USB ou batterie externe

---

### 🔌 Les circuits

#### 🔹 Circuit en série 
![circuit en série](/420-411-Interfaces-Humain-Machine/images/circuit-serie.jpg)


#### 🔹 Circuit parallèle 
![circuit parallèle](/420-411-Interfaces-Humain-Machine/images/circuit-parallel.jpg)