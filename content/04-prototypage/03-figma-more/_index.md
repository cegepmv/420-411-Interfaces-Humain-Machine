+++
title = "Prototypage avec Figma (Avancé)"
weight = "3"
draft = "false"
+++

---

## Effets (demo)

- Ombre Interne
- Ombre portée
- Calque de floutage
- Flou de fond
- Bruit
- Texture
- Verre

---

## Masques (demo)

1) Masque Avatar

<img src="/420-411-Interfaces-Humain-Machine/images/AvatarMask.png" alt="Avatar Mask" width="300">

2) Masque de texte

<img src="/420-411-Interfaces-Humain-Machine/images/TextMask.png" alt="Text Mask" width="300">

3) Image avec arrière plan transparent

<img src="/420-411-Interfaces-Humain-Machine/images/TransparentMask.png" alt="Transparent Mask" width="300">

## Responsive Design : Auto Layout + Contraintes (demo)

L’Auto Layout dans Figma est une fonctionnalité qui permet d’organiser automatiquement les éléments dans un conteneur, un peu comme un système de mise en page intelligent. Au lieu de placer les objets manuellement, Auto Layout gère l’alignement, les espacements et le redimensionnement automatiquement.

On peut organiser les éléments de façon **verticale**, **horizontale** ou sous format de **grille** et contrôler les **"paddings"** et les **"gaps"**.

Les contraintes (Constraints) servent à définir comment un élément se comporte quand on redimensionne son frame parent.

#### Types de contraintes

🔹 Horizontal

Définit la position gauche/droite
- Left → reste collé à gauche
- Right → reste collé à droite
- Left & Right → s’étire horizontalement
- Center → reste centré
- Scale → se redimensionne proportionnellement

🔹 Vertical

Même principe en haut/bas
- Top
- Bottom
- Top & Bottom → s’étire en hauteur
- Center
- Scale

---

## Composantes et styles (demo)

Les composantes (Components) sont des éléments réutilisables que tu peux utiliser plusieurs fois dans un design sans tout recréer.

> Une composante = un élément que tu crées une fois et que tu réutilises partout.

#### Les 2 types importants
1. Main component (composant principal) : C’est l’original, si on l’édite, toutes les instances seront modifiées.

2. Instance : une copie liée au composant principal. On peut la modifier comme on veut mais elle reste liée au composant principal.

> Les styles c'est comme les composantes mais pour des couleurs, des polices...
---

## Animations (prototype demo)

Un prototype permet de transformer un design statique en interface interactive simulant une vraie application.

---

## Exercice 1

Générez le frame suivant : 

[hero.png](/420-411-Interfaces-Humain-Machine/images/hero.png)

[background.png](/420-411-Interfaces-Humain-Machine/images/background.png)

<img src="/420-411-Interfaces-Humain-Machine/images/SongPlayer.png" alt="Song Player" width="300">

## Exercice 2

En groupes de 2 étudiants, tirez au sort une idée de business et créez les prototypes de son application mobile.

- Il doit y avoir au moins 6 calques (frames)
- Les calques doivent être reliés entre eux par des animations
- Vous devez utiliser les contraintes et le auto-layout là où il faut
- Vos prototypes doivent contenir au moins un masque
- Vos prototypes doivent contenir au moins un effet par calque

Vous allez ensuite présenter votre travail en classe sous format "Prototype"