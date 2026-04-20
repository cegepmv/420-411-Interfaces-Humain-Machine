+++
title = "Mouvements joueur et physique 2D"
weight = "2"
+++

## Ajouter un "Player"
Un player peut être un sprite importé ou un game object créé manuellement.

On ajoute un script pour le faire bouger :
```csharp
using UnityEngine;

public class PlayerMouvement : MonoBehaviour
{
    public float speed = 5f;
    // Update is called once per frame
    void Update()
    {
        float move = Input.GetAxisRaw("Horizontal");

        transform.position += new Vector3(move * speed * Time.deltaTime, 0f, 0f);
    }
}
```
## Ajouter un "Rigidbody2D"
Un Rigidbody, c’est le composant qui dit à Unity : “Cet objet doit être géré par la physique”.

Quand tu l’ajoutes, Unity peut :  
**- appliquer la gravité :** l’objet tombe tout seul  
**- détecter les collisions :** murs, sol, autres objets  
**- appliquer des forces**  
**- gérer la vitesse**  

Player > Add Component > Physics 2D > Rigidbody 2D (freeze position sur l'axe Z)

## Ajouter un "Collider 2D"
Un Collider2D, c’est une zone invisible autour d’un objet qui permet à Unity de détecter :

- les collisions (mur, sol, obstacles)
- les contacts entre objets

**Les principaux types de collider**  
- BoxCollider2D  
- CircleCollider2D  
- CapsuleCollider2D  
- PolygonCollider2D  
...


<p style="color:red;font-weight: bold; font-size: 25px;">==> Bougeons le player avec son rigidbody maintenant !</p>

```csharp
using UnityEngine;

public class PlayerMouvement : MonoBehaviour
{
    public float speed = 5f;
    private Rigidbody2D rb;
    private float move;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        move = Input.GetAxisRaw("Horizontal");
    }

    void FixedUpdate()
    {
        rb.linearVelocity = new Vector2(move * speed, rb.linearVelocity.y);
    }
}
```

<p style="color:red;font-weight: bold; font-size: 25px;">Et si on veut inverser (Flip) le joueur ?</p>

```csharp
// Flip du personnage
    if (move > 0)
    {
        transform.localScale = new Vector3(1, 1, 1);
    }
    else if (move < 0)
    {
        transform.localScale = new Vector3(-1, 1, 1);
    }
```
## Faire sauter le "Player"

```csharp
using UnityEngine;

public class PlayerMouvement : MonoBehaviour
{
    public float speed = 5f;
    public float jumpForce = 5f;
    private Rigidbody2D rb;
    private float move;
    private bool isGrounded = true;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        move = Input.GetAxisRaw("Horizontal");

        // Flip du personnage
        if (move > 0)
        {
            transform.localScale = new Vector3(1, 1, 1);
        }
        else if (move < 0)
        {
            transform.localScale = new Vector3(-1, 1, 1);
        }

        // jump
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);
        }
    }

    // Detect when touching ground
        void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
        }
    }

    // Detect when leaving ground
    void OnCollisionExit2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = false;
        }
    }
    
    void FixedUpdate()
    {
        rb.linearVelocity = new Vector2(move * speed, rb.linearVelocity.y);
    }
}
```
<p style="color:red;font-weight: bold; font-size: 25px;">Et si mon jeu est de type top-down runner ?</p>

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float speed = 5f;
    private Rigidbody2D rb;
    private Vector2 moveInput;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Input (horizontal + vertical)
        moveInput.x = Input.GetAxisRaw("Horizontal");
        moveInput.y = Input.GetAxisRaw("Vertical");

        // normalize so diagonal isn't faster
        moveInput = moveInput.normalized;
    }

    void FixedUpdate()
    {
        rb.linearVelocity = moveInput * speed;
    }
}
```
<p style="color:red;font-weight: bold; font-size: 25px;">Et si je veux que la caméra suit le joueur ?</p>

```csharp
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform player;
    public float smoothSpeed = 5f;
    public float yOffset = 1.5f;

    void LateUpdate()
    {
        Vector3 targetPosition = new Vector3(
            player.position.x,
            player.position.y + yOffset,
            transform.position.z
        );

        transform.position = Vector3.Lerp(
            transform.position,
            targetPosition,
            smoothSpeed * Time.deltaTime
        );
    }
}
```

## Collecte d’objets

* Ajoutez l'item à collecter avec un collider2D.
* Cochez Is Trigger ✅ dans le collider (On utilise Trigger pour ne pas bloquer le joueur). 
* Sur l'item à collecter, ajoutez le script suivant :

```csharp
using UnityEngine;

public class CollectItem : MonoBehaviour
{
    public int scoreValue = 1;

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Debug.Log("Item collected!");

            // augmenter score (exemple simple)
            ScoreManager.instance.AddScore(scoreValue);

            // détruire l'objet
            Destroy(gameObject);
        }
    }
}
```
* Ajouter un game object vide dans votre scène appelé "ScoreManager" et attachez-y le script suivant :

```csharp
using UnityEngine;

public class ScoreManager : MonoBehaviour
{
    public static ScoreManager instance;
    public int score = 0;

    private void Awake()
    {
        instance = this;
    }

    public void AddScore(int value)
    {
        score += value;
        Debug.Log("Score: " + score);
    }
}
```
## Ennemis / interactions de base

* Ajoutez l'ennemi avec un collider2D et un rigidbody2D (body type = kinematic).
* Cochez Is Trigger ✅ dans le collider (On utilise Trigger pour ne pas bloquer le joueur). 
* Sur l'ennemi, ajoutez le script suivant :
```csharp
using UnityEngine;

public class EnemyDamage : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Debug.Log("Player hit enemy!");

            // exemple simple : restart scène
            UnityEngine.SceneManagement.SceneManager.LoadScene(
                UnityEngine.SceneManagement.SceneManager.GetActiveScene().name
            );
        }
    }
}
```

## Animations

Demo en classe.
