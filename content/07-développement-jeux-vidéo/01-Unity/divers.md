+++
title = "Annexes Diverses"
weight = "4"
+++

## Ajouter un audio dans ton jeu  
**Ajouter une musique de fond :**  
- Importez le fichier audio à utiliser (mp3, wav...) dans le dossier Assets
- Dans la scène → clic droit → Create Empty
- Renommez le game object : MusicManager (ou AudioManager)
- Ajoutez un component : Audio Source et glissez l'Audio Clip dans le champ Audio Generator.
- Cochez :
    * Loop
    * Play On Awake (lancer automatiquement)

**Ajouter un son à un moment précis :**  
On se propose d'ajouter un son d'effort quand le joueur saute.  
Dans le script du Player, ajoutez :

```csharp
public AudioClip jumpSound;
private AudioSource audioSource;
.
.
.
// jump
    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
    {
        rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);
        audioSource = GetComponent<AudioSource>();
        audioSource.PlayOneShot(jumpSound);
    }
```
Dans le champ "jumpSound", glissez le fichier audio du son d'effort. Ceci jouera le son à chaque fois le player saute.

## Créer un jeu à plusieurs niveaux (multilevel)
- Créer un jeu multi-level dans Unity, ça revient surtout à gérer plusieurs scènes et un système pour passer de l’une à l’autre.
- Chaque niveau = une Scene (Level1, Level2, Level3, LevelBonus...)
- File → Build Profiles → Scene List → Ajouter toutes les scènes avec leurs build index
- Passer d'une scène à la suivante :
```csharp
SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex + 1);
```
Le passage d'un niveau à l'autre peut dépendre d'une condition :
- le joueur touche une porte
- le joueur arrive à un checkpoint
- le joueur bat un boss...

## Exporter le jeu
Dans Unity , exporter (ou “build”) un jeu veut dire transformer ton projet Unity (éditeur) en application jouable.  
- un fichier .exe (Windows)
- une app Mac
- un jeu console
- ou une version web

**Étapes générales :**
- File → Build Profiles
- Choisissez la plateforme (PC, Web, etc.)
- Cliquez sur Build
- Unity génère un dossier avec le jeu

> Vous pouvez même monétiser votre jeu maintenant (itch.io, steam...) :)

## Remise de travaux en jeu 2D (Unity)
Un projet Unity est structuré de façon à ce que chaque dossier ait un rôle bien précis. Certains sont destinés à être modifiés par vous, tandis que d’autres sont purement internes et ne doivent pas être touchés.

**Assets/**

C’est le cœur de votre projet — le seul dossier que vous êtes vraiment censé modifier directement. Il contient tout le contenu de votre jeu : scripts, scènes, prefabs, textures, modèles, audio, etc. Tout ce que vous importez dans Unity se retrouve ici. Unity génère également des fichiers .meta à côté de chaque ressource pour suivre les identifiants et les paramètres.

**Library/**

Considérez-le comme le cache de Unity. Il stocke les versions importées/traitées de vos ressources, les compilations de shaders, ainsi que d’autres données intermédiaires qui permettent à Unity de fonctionner plus rapidement. Vous ne devez pas le modifier manuellement, et il peut être supprimé sans risque — Unity le recréera lors de la réouverture du projet (cela peut toutefois prendre du temps).

**Logs/**

Ce dossier contient les fichiers de journal générés par Unity — utiles pour diagnostiquer les plantages, erreurs ou problèmes de performance. En cas de souci, c’est souvent ici que vous trouverez des indices.

**Packages/**

Ce dossier gère les dépendances via le Unity Package Manager. Il liste les packages utilisés par votre projet (comme les systèmes d’entrée, pipelines de rendu, etc.). Le fichier manifest.json qu’il contient définit ces dépendances.

**ProjectSettings/**

Il contient toute la configuration globale du projet : paramètres graphiques, physique, entrées, tags, layers, options de build, etc. Ces fichiers sont essentiels et doivent généralement être versionnés, car ils définissent le comportement du projet.

**UserSettings/**

Ce dossier stocke les préférences spécifiques à votre machine/utilisateur — comme la disposition de l’éditeur ou certaines préférences locales. Il n’est pas destiné à être partagé en équipe et est généralement ignoré dans le versionnement.

<p style="color:red;font-weight: bold; font-size: 20px;">Avant de remettre votre jeu, assurez-vous d'avoir supprimé le dossier Library avant de compresser le dossier</p>
