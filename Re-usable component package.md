# Lootable chest unity package

## Description

Here I will explain how to use the lootable chest unity package and how it works.

When the player is next to the chest, with the press of a single button the chest will open and throw collectable coins next to it.

## 1. Game Objects used

In an empty game object called `Chest` I added:

`chest_bottom` which is the 3D model of the lower part of the chest.

`chest_lid_hinge` which we will use to rotate the lid in an animation.

`chest_lid` which is a child of `chest_lid_hinge` and it's the 3D model of the lid.

`loot_drop` which has the scripts necessary.

`spawn_point` which is the spawnpoint of the coins inside the chest.

`coin` which is the prefab of the coins that we need to spawn with a script attached to it.

## 2. Scripts used

I used 3 scripts:

`InteractOpen` which checks if the player is in the range of the chest, and if the player presses F on the keyboard the opening animation will play.
```
public GameObject chestLidHinge;
    public Animator _animator;
    public bool _inrange;

    private void Start()
    {
        _animator = chestLidHinge.GetComponent<Animator>();
        _inrange = false;
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.tag == "Player")
        {
            _inrange = true;
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.tag == "Player")
        {
            _inrange = false;
        }
    }

    private void OnTriggerStay(Collider other)
    {
        if (Input.GetKeyDown(KeyCode.F) && _inrange)
        {
            _animator.SetBool("PlayerOpen", true);
        }
    }
    
```
`DropLoot` is used to check if the chest was already looted or not. If the answer is no, the script will spawn the X amount of coins in the script, in this case 50, and it will use a big force to spread the coins around the chest.
```
public GameObject coin;
    public GameObject spawnPoint;
   

    private bool isLooted;

    void Start()
    {
        isLooted = false;
     
    }

    private void OnTriggerStay(Collider other)
    {
        if (!isLooted && other.tag == "Player" && Input.GetKeyDown(KeyCode.F))
        {
            for (int i = 0; i < 50; i++)
            {
                StartCoroutine(CoinSpawn());
            }
            isLooted = true;
        }
    }

    IEnumerator CoinSpawn()
    {
        
        yield return new WaitForSeconds(1f);
        GameObject newCoin = Instantiate(coin, spawnPoint.transform.position, coin.transform.rotation);
        Rigidbody rb = newCoin.GetComponent<Rigidbody>();
        rb.AddForce(Random.onUnitSphere * 1000.0f, ForceMode.Impulse);
        
        
    }
 ```
`ItemPickup` is used on the coin. If the player touches the coin, it will disappear.
```
  private Collider CoinCollider;
    float direction;

    [SerializeField]
    float speed = 5f;
    [SerializeField]
    float height = 0.5f;

    Vector3 pos;

    void Start()
    {
        CoinCollider = GetComponent<Collider>();
        pos = transform.position;
    }

    void Update()
    {
        transform.Rotate(0, 0, 90 * Time.deltaTime);
        float newY = Mathf.Sin(Time.time * speed) * height + pos.y;
        transform.position = new Vector3(transform.position.x, newY, transform.position.z);
    
    }

   
    private void OnTriggerEnter(Collider other)
    {
        if (other.tag == "Player")
        {
            Destroy(this.gameObject);
        }
    }

```

## 3. Additional components used in scripts

`spawn_point` is used in the `DropLoot` script and it's used as the location where the coins should spawn.

I also added the animation to `chest_lid_hinge`, which will rotate the lid of the chest around the hinge.

Attached to the `loot_drop` game object I also added a trigger collider which will determine if the player is in the range of the chest or not.

## Wrapping up

With all the components stated above, and with the scripts that have a connection between them on the same game object, the chest will open when the player presses `F` while next to the chest.

After that, the player can collect all the coins.
