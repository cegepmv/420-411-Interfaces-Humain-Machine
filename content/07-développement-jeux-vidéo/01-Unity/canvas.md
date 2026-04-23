+++
title = "Interfaces en jeux vidéo"
weight = "3"
+++

## Types d'interfaces dans les jeux vidéo  
**HUD(in game)**  
- vies
- score
- barre de vie

> toujours visible pendant le jeu
> Le HUD sert à informer le joueur, à donner du feedback et à l'aider à prendre des décisions.  

**Menus**
- menu principal
- pause
- game over

> navigation + décisions

**Inventaire / systèmes**
- coffre
- objets collectés

> interaction + gestion

## Principes UX appliqués au jeu

**Lisibilité**  
- texte clair
- tailles adaptées

**Feedback immédiat**  
- perdre de la vie → animation / changement visuel
- collecter → compteur qui augmente

**Minimalisme**  
- ne pas surcharger l’écran

**Hiérarchie visuelle**  
- info importante → visible en premier
ex: vie > score

**Cohérence**  
- mêmes couleurs, mêmes icônes

**Accessibilité**  
- couleurs visibles
- taille suffisante

## Les états du jeu

🎮 Playing → le jeu tourne  
⏸️ Paused → le jeu est figé  
💀 Game Over → fin (échec)  
🏠 Menu → navigation  

## Créer des composantes UI dans un jeu vidéo
**Exemple 1 : Text (score)**

<p style="font-weight:bold;width: 190px;color: #000;background-color: #ffcf33;">1/ Créer un Canvas UI : </p> 
GameObject → UI → Canvas

<p style="font-weight: bold; width: 280px; color: #000; background-color: #ffcf33;">2/ Ajouter un texte pour le score :  </p>

- Clic droit sur Canvas → UI → Text - TextMeshPro (Clique sur Import TMP Essentials si demandé)  
- Modifier le texte = Score : 0  

<p style="font-weight: bold; width: 370px; color: #000; background-color: #ffcf33;">3/ Positionner le score dans RectTransform :  </p>
Clique sur les ancres (petit carré) et choisis Top Left (haut gauche) puis ajuste : Pos X et Pos Y.

<p style="font-weight: bold; width: 170px; color: #000; background-color: #ffcf33;">4/ Styliser le texte :  </p>
Font Size → 24–36
Couleur → blanc (ou autre)

<p style="font-weight: bold; width: 210px; color: #000; background-color: #ffcf33;">5/ Lier le texte au script :  </p>
Glisse le texte UI dans : Score Text (dans Inspector) du score manager

**Exemple 2 : Image (nombre de vies)**

1/ Ajouter l'image du coeur (sprite 2D) : Right click → UI → Image  
2/ Ajouter le nombre de vies (3 par exemple) : Right click on Canvas → UI → Text - TextMeshPro  
3/ Positionner les éléments en haut à droite par exemple  
4/ Créer un LifeManager (GameObject vide) avec le script suivant :
```csharp
using UnityEngine;
using TMPro;

public class LifeManager : MonoBehaviour
{
    public TextMeshProUGUI lifeText;
    int lives = 3;

    void Start()
    {
        UpdateUI();
    }

    public void LoseLife()
    {
        lives--;
        UpdateUI();

        if (lives <= 0)
        {
            Debug.Log("Game Over");
            // ici tu peux afficher menu game over
        }
    }

    void UpdateUI()
    {
        lifeText.text = lives.ToString();
    }
}
```

5/ Glisser le texte de nombre de vie dans la variable LifeText.  
6/ Modifier le script de l'ennemi :

```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    if (collision.gameObject.CompareTag("Player"))
    {
        FindObjectOfType<LifeManager>().LoseLife();
    }
}
```

**Exemples 3 + 4 : Panel (groupes UI) + Button (menu Game Over)**

- Clic droit → UI → Panel
- Renomme-le : GameOverPanel
- Désactive-le au départ (décoche le GameObject dans l’Inspector)
- Ajoute dedans :
Text : “Game Over”
Button : “Rejouer”
(optionnel) Button : “Quitter”
- Crée un script GameManager.cs :
```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public GameObject gameOverPanel;

    public void GameOver()
    {
        gameOverPanel.SetActive(true);
        Time.timeScale = 0f; // stop le jeu
    }

    public void Restart()
    {
        Time.timeScale = 1f; // remet le jeu normal
        SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
    }
}
```

- Crée un empty GameObject → GameManager
- Ajoute le script comme component
- Glisse GameOverPanel dans le champ du script
- Dans le bouton : OnClick() : Ajoute GameManager
- Choisis la fonction : GameManager → Restart()
- Déclencher Game Over

Exemple dans un script de LifeManager :
```csharp
if (lives <= 0)
{
    FindObjectOfType<GameManager>().GameOver();
}
```
**Exemple 5 : Slider (barre de vie)**

- Ajoute un Slider dans ton Canvas
Mets :
Min Value = 0
Max Value = vie max (ex: 100)
- Désactive “Interactable” (car c’est une barre, pas un contrôle)
- Script de vie du joueur (sur Player)
```csharp
using UnityEngine;
using UnityEngine.UI;

public class PlayerHealth : MonoBehaviour
{
    public int maxHealth = 100;
    public int currentHealth;

    public Slider healthSlider;

    void Start()
    {
        currentHealth = maxHealth;
        healthSlider.maxValue = maxHealth;
        healthSlider.value = currentHealth;
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;

        if (currentHealth < 0)
            currentHealth = 0;

        healthSlider.value = currentHealth;
    }
}
```
- Détecter la collision avec un ennemi

Sur ton ennemi :

```csharp
using UnityEngine;

public class EnemyDamage : MonoBehaviour
{
    void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            PlayerHealth playerHealth = collision.gameObject.GetComponent<PlayerHealth>();

            if (playerHealth != null)
            {
                playerHealth.TakeDamage(10);
            }
            else
            {
                Debug.LogWarning("PlayerHealth not found on Player!");
            }
        }
    }
}
```