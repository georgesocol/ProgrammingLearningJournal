# Bullet Shooting Gun Script Tutorial

## Description

In this tutorial we will create a script that you can attach to 2D object and transform it into a gun shooting the player while on Play Mode.

## 1. Create a new scene

Start by creating a new scene.

Add a 2D square, I am going to call it Gun.
## 2. Add the components

Add a Sprite Renderer on the objects. 


## 3. Create the script

Create a new script named BulletGun and attach it to the Square.

First, we need to add the variables that we are going to use.
```
    public float range;
    public Transform target;
    Vector2 direction;
    public GameObject gun;
    public GameObject bullet;
    public float fireRate;
    public Transform shootPoint;
    public float bulletSpeed;
    bool detected;
    public float nextTimeToFire;
    RaycastHit2D hit;
    public LayerMask player;
```
We will use the float named range to choose how far the player can be seen by the turret.

We will use Transform target to check the player's position.

We will use Vector2 Direction to check where the gun will be pointed.

We will use float fireRate to choose how fast the turret will shoot.

We will use Transform shootPoint as the point where bullets instantiate.

We will use float bulletSpeed to change the speed of the bullet.

We will use bool detected to check if the player is in turret's range.

We will use float nextTimeToFire to make the turret shoot in rounds and not non-stop.


## 4. Void Update()

We will start working in the void Update() function now.

First we will let the turret move after the player when in range.
```
 Vector2 targetposition = target.position;
        direction = targetposition - (Vector2)transform.position;
        gun.transform.up = direction;
        CheckIfPlayer();
```


## 5. void CheckIfPlayer()


```
hit = Physics2D.Raycast(transform.position, direction, range, player);
        detected = hit ? true : false;
        if (detected)
        {
            if (hit.rigidbody == target.GetComponent<Rigidbody2D>() && (Time.time > nextTimeToFire))
            {

                nextTimeToFire = Time.time + 1 / fireRate;
                shoot();
            }
        }
```
This function is used to trace a ray towards the player. If the player is hit and enough time passed after the last time the gun shot, the `shoot()` function will be called.


##6. void shoot()

This function instantiates the bullets which will move towards the player.
```
              GameObject BulletIns = Instantiate(bullet, shootPoint.position, gun.transform.rotation);
              BulletIns.GetComponent<Rigidbody2D>().velocity = direction * bulletSpeed;
```


##7. void OnDrawGizmosSelected()

This function is used to draw the range of the turret and to check if the player is inside said range.

```
Gizmos.DrawWireSphere(transform.position, range);

```
## 8. Test

Now you can test if the script works by playing the scene and moving the player next to the turret.
