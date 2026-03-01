+++
title = "Programmation d'arduino"
weight = "2"
+++

L'IDE Arduino vous permet d'écrire des programmes et de les mettre dans votre Arduino. Il peut être téléchargé depuis arduino.cc/download

- Arduino est programmé en C / C++

- Mais la plateforme simplifie beaucoup de choses :

* Pas besoin d’inclure toutes les bibliothèques standard

* Fonctions comme pinMode(), digitalRead(), analogRead(), Serial.print() déjà prêtes

## 1) Structure d’un programme Arduino

```cpp
void setup() {
  // Exécuté une seule fois au démarrage
}

void loop() {
  // Exécuté en boucle infinie
}
```

### Exemple 

```cpp
const int ledPin = 13;
const int buttonPin = 2;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  if(digitalRead(buttonPin) == HIGH){
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
}
```
> Créeons le circuit qui peut tester ce programme.

## 2) Syntaxe de base 
* Déclaration des variables :

```cpp
int ledPin = 13;        // entier pour stocker numéro de pin
float temperature = 0;  // nombre à virgule pour la température
bool buttonState = false; // vrai/faux pour état bouton
```
Types basiques : int, float, bool, char, String

* Contrôle des pins :

a) Définir le mode d’une pin
```cpp
pinMode(13, OUTPUT); // sortie (LED)
pinMode(2, INPUT);   // entrée (bouton)
```

b) Lire une pin digitale
```cpp
int state = digitalRead(2); // HIGH ou LOW
```

c) Écrire sur une pin digitale
```cpp
digitalWrite(13, HIGH); // allume LED
digitalWrite(13, LOW);  // éteint LED
```

d) Lire une pin analogique
```cpp
int value = analogRead(A0); // 0 à 1023
```

e) Sortie PWM (simule analogique)
```cpp
analogWrite(9, 128); // 0 → 255
```

* Communication série :

```cpp
Serial.begin(9600);        // initialise le port série
Serial.print("Valeur = "); // affiche sans retour ligne
Serial.println(value);     // affiche avec retour à la ligne
```
* Structures de contrôle :

a) Conditionnelles
```cpp
if (temperature > 27) {
  digitalWrite(13, HIGH);
} else {
  digitalWrite(13, LOW);
}
```

b) Boucles
```cpp
for(int i = 0; i < 10; i++) {
  digitalWrite(13, HIGH);
  delay(500);
  digitalWrite(13, LOW);
  delay(500);
}

while(digitalRead(2) == LOW) {
  // attendre que le bouton soit appuyé
}
```

## 3) Bonnes pratiques :

- Toujours déclarer les pins et variables en haut du programme

- setup() = initialisation, loop() = exécution répétée

- Utiliser des commentaires pour expliquer le code

- Lire et afficher les valeurs avec Serial.print() pour débogage

## 4) Exercices : 

**1/ Allumer une LED :**

- Connecter la LED à la pin 13 via une résistance 
- Faire clignoter la LED toutes les 1 seconde

**2/ Intensité variable d’une LED (PWM) :**

- Faire varier la luminosité de la LED de faible à forte progressivement

**3/ Piano avec buzzer :**

- En utilisant le buzzer passif que vous avez dans le kit :

* Vous allez faire un circuit avec le buzzer et sept boutons (Do, ré, mi, fa, sol , la , si). 
* Le buzzer et les boutons seront chacun connectés à un pin d'arduino. 
* Le clic sur l'un des boutons va jouer la note correspondante pendant 500ms. 
* Utilisez la fonction `tone(buzzerPin, frequency, duration)` pour jouer la note en question. 
* Utilisez la fonction `noTone(buzzerPin)` pour arrêter le son. 

Les différentes fréquences des notes :
| Note                   | Fréquence (Hz) |
| ---------------------- | -------------- |
| Do (C4)                | 261            |
| Ré (D4)                | 294            |
| Mi (E4)                | 330            |
| Fa (F4)                | 349            |
| Sol (G4)               | 392            |
| La (A4)                | 440            |
| Si (B4)                | 494            |
| Do (C5)                | 523            |


