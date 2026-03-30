+++
title = "Développement Front End"
type = "chapter"
weight = 6
pre = "6."
+++

**Notre objectif est de concevoir une interface web permettant :**  

- d’afficher les données provenant d’un système Arduino via une API
- d’interagir avec ce système en contrôlant une pompe à eau  

**I) Contexte**  

Un backend (Node.js) vous sera fourni dans les séances prochaines et qui est accessible via : http://localhost:3001/ et expose les routes suivantes :

- GET /api/data → retourne les données des capteurs
- POST /api/pump → déclenche la pompe à eau

**II) Format des données :**  
{  
  "temp": 28.4,  
  "hum": 41,  
  "soil": 52  
}

**III) Travail demandé**  
Vous devez créer une application web sur une seule page permettant :

**1) Affichage des données (3 cartes)**

Afficher les informations suivantes :

- 🌡️ Température ambiante  
- 💧 Humidité ambiante  
- 🌱 Humidité du sol  

**Contraintes :**  
- Les données doivent être récupérées depuis /api/data
- Les valeurs doivent être mises à jour automatiquement toutes les 60 secondes
- Chaque information doit être affichée dans une composante visuelle distincte (carte)

**2) Bouton de contrôle de la pompe**

**Créer un bouton :** "Start Pump"

**Fonctionnement :**  
- Envoie une requête POST vers /api/pump
- Affiche une confirmation (message ou alerte)

**3) Si vous utilisez React**

Votre interface doit être construite en composantes réutilisables. Créer au minimum :
- une composante Card
- une composante Button
- Utiliser les hooks (useState, useEffect)

**4) Interface utilisateur**

Votre interface doit :

- contenir un titre principal
- afficher les 3 cartes alignées
- contenir un bouton
- être visuellement claire (CSS minimal requis)

