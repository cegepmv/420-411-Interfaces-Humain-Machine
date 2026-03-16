+++
title = "Utilisation de capteurs"
weight = "3"
+++

Dans notre projet, nous avons besoin des informations de température et d'humidité pour les afficher sur notre dashboard.  
Ces informations seront lues grâce à **des capteurs**, qui transforment une grandeur physique (température, humidité…) en signal électrique.  
La carte Arduino va ensuite analyser ces informations et envoyer des commandes à **un actionneur**, comme une pompe ou une LED.  


### 1) Capteur température et humidité DHT11 :  
![connexion DHT11](/420-411-Interfaces-Humain-Machine/images/DHT11.png)

- Le DHT11 est un capteur de température et d'humidité très populaire, facile à utiliser et abordable. Il peut mesurer des températures de 0 à 50°C avec une précision de ±2°C, et des humidités de 20 à 90% avec une précision de ±5%.  
- Il utilise un protocole de communication numérique pour transmettre les données à la carte Arduino, ce qui le rend simple à interfacer.  
- Le DHT11 est idéal pour les projets de base qui nécessitent des mesures de température et d'humidité, mais il peut ne pas être suffisamment précis pour des applications plus exigeantes.

#### Connexion et utilisation du DHT11 :

**Connecter le capteur DHT11 :**

- VCC → 5V
- GND → GND
- DATA → pin digitale

**Installer la librairie**

```cpp
Sketch → Include Library → Manage libraries → DHT sensor library → INSTALL
```

**Ecrire le programme**

- Importer une librairie :
```cpp
#include <DHT.h>
```

- Créer un objet capteur DHT :
```cpp
DHT dht(DHTPIN, DHTTYPE);
```

- Utiliser les fonctions nécessaires pour lire les valeurs de température en Celcius et d'humidité en % :
```cpp
dht.begin();
dht.readHumidity();// doit être lue toute les 2 secondes
dht.readTemperature();
```

- Brancher le capteur et écrire et tester le programme qui lit et affiche la moyenne de température et la moyenne d'humidité  sur 1 minute (la moyenne de 30 valeurs, une valeur par 2 secondes).

### 2) Capteur d'humidité du sol : 
![Soil moisture sensor](/420-411-Interfaces-Humain-Machine/images/sensor-in-soil.png)

Le capteur d’humidité du sol sert à mesurer la quantité d’eau présente dans la terre.  

La terre humide conduit mieux l’électricité que la terre sèche.
- **Sol sec** → résistance électrique élevée
- **Sol humide** → résistance électrique faible

Le capteur utilise deux électrodes métalliques plantées dans la terre. L’Arduino envoie un petit courant entre ces électrodes. Selon l’eau dans le sol, la tension mesurée change.

**Valeurs typiques**

Ça dépend du type de capteur, dans notre cas c'est des capteurs reversés. Les valeurs sont entre 0 et 1023 :  

- sol très humide → valeur > 800
- sol normal → valeur ≈ 500
- sol sec → valeur <≈ 300-400

👉 plus la valeur est grande → plus le sol est humide.

**Connecter le capteur :**
- VCC → 5V
- GND → GND
- AO → Pin analogique

**Ecrire le programme**  
- Brancher le capteur et écrire et tester le programme qui lit et affiche la moyenne d'humidité du sol sur 1 minute (la moyenne de 30 valeurs, une valeur par 2 secondes). Cette moyenne doit être affichée sous format d'un pourcentage (0→0% et 1023→100%)

### 3) Commander une pompe à eau :  
![pompe à eau](/420-411-Interfaces-Humain-Machine/images/pompe.png)
La pompe doit être commandée avec :
- transistor  
![transistor](/420-411-Interfaces-Humain-Machine/images/transistor.png)
- diode de protection  
![diode](/420-411-Interfaces-Humain-Machine/images/diode.png)

**Connecter la pompe :**
- pin digitale → résistance → pin à gauche de transistor
- pompe (+) → alimentation externe (batterie 9V)
- pompe (-) → pin au milieu de transistor
- transistor pin à droite → GND Arduino
- diode en parallèle sur la pompe

**Ecrire le programme**  
- Brancher la pompe et écrire un programme qui lance la pompe une fois un bouton est cliqué.