# 🌱 Projet Arduino – Plante Connectée

![Architecture projet](/420-411-Interfaces-Humain-Machine/images/project-overview.png)
## 🎯 Objectif

Créer un système intelligent capable de :

- Mesurer la température et l’humidité de l’air
- Mesurer l’humidité du sol
- Indiquer l’état de la plante avec des LEDs
- Afficher les données sur un dashboard (ordinateur)
- Contrôler une pompe à eau à distance

---

## 🧩 Composants utilisés

### 🔹 Arduino Uno
![Arduino Uno](https://upload.wikimedia.org/wikipedia/commons/3/38/Arduino_Uno_-_R3.jpg)

👉 Rôle :
- Cerveau du système
- Lit les données des capteurs
- Contrôle les LEDs et la pompe
- Communique avec l’ordinateur

---

### 🌡️ Capteur DHT11 (Température / Humidité)
![DHT11](https://cdn3.botland.store/61090-pdt_540/temperature-and-humidity-sensor-dht11-module-iduino-se052.jpg)

👉 Rôle :
- Mesure la température ambiante (°C)
- Mesure l’humidité de l’air (%)

---

### 🌱 Capteur d’humidité du sol
![Soil Moisture Sensor](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRo3xm_4pB3kIWrCHPgsxoFvP0Rxz5Y6GoGHA&s)

👉 Rôle :
- Détecte si le sol est sec ou humide

---

### 🔴 LED Rouge
![Red LED](https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcQ-4mPsTZqVDs7c5grdBo880zg4aLpqJokboA-oeTyLZQch4PTwAO6OJdmkzJaL0Y7cJ_HTqs4bIWKqBVkoP4hCylGNRJKSyND6AZ9RpotDHaxgQQxCDlvxYCV5Cpj6hM5or0S-Ow&usqp=CAc)

👉 Rôle :
- S’allume si la température est trop élevée

---

### 🔵 LED Bleue
![Blue LED](https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcQphB4AzUJ2lAqagpB2eEN9kuyT-rZGE_uDkpqXXaAPYSNM0sp6d5YoLOkD-5i05S18Pi4RaDYDYg2iEWKMB2HJcTl4XslExgGzgk5ay4hxiWfc-3y_BMEDrqikvvH4TJO8MiGNEstWiAs&usqp=CAc)

👉 Rôle :
- S’allume si le sol est sec

---

### 💧 Pompe à eau
![Water Pump](https://encrypted-tbn2.gstatic.com/shopping?q=tbn:ANd9GcQ-6tXqCTEHZSyUywsWINcKvPsAFGAleBKzuWoHE9HcV9cJIv-arX1rLbwpLMsmg3SlR0PeMr27iZ7xaRshELXez2kobTvJXIsTL5ftTiCBsubvGnzqLejbiq_XcYi8rRqmJgSbkA&usqp=CAc)

👉 Rôle :
- Arroser la plante automatiquement

---

### 💻 Ordinateur (Dashboard React + backend NodeJS)

👉 Rôle :
- Afficher les données en temps réel
- Permettre à l’utilisateur d’activer/désactiver la pompe

---

## 🔌 Fonctionnement du système

1. Les capteurs mesurent l’environnement
2. Arduino lit les valeurs
3. Arduino :
   - allume les LEDs selon les conditions
   - contrôle la pompe
   - envoie les données via USB
4. L’ordinateur reçoit les données
5. Le dashboard :
   - affiche les informations
   - envoie une commande pour activer la pompe

---

## ⚙️ Conditions du projet

- Température > 30°C → 🔴 LED rouge ON
- Sol sec (humidité du sol < 40 %) → 🔵 LED bleue ON
- Bouton dashboard → 💧 pompe ON/OFF

---

## 🔄 Communication

👉 Bidirectionnelle :

- Arduino → Dashboard (données capteurs)
- Dashboard → Arduino (commande pompe)

---