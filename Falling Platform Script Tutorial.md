# Falling Platform Script Tutorial

## Description

In this tutorial we will create a script that you can attach to an object and transform it into a falling platform when the player jumps on it in Play Mode.

## 1. Create a new scene

Start by creating a new scene.

Add a Collider with trigger on an object, I am going to call it FallingPlatform.
## 2. Add the components

Add a Rigidbody on the object. 


## 3. Create the script

Create a new script named FallingPlatform and attach it to the object.

First, we need to add the variables that we are going to use.
```
    public GameObject player;
    public float FallWaitingTime;
    private Rigidbody rb;
```

We will use GameObject player to check if the player is standing on the platform.

We will use float FallWaitingTime to choose after what time after the trigger the platform will fall. 

We will use Rigidbody rb to set active object's gravity once collider being triggered. 



## 4. private void Start()

We will start working in the void Start() function now.

First we will let the platform trigger when the player touches it.
```
 private void Start()
    {
        rb = GetComponent<Rigidbody>();
        rb.useGravity = false;
    }
    private void OnTriggerEnter(Collider other)
    {
        if (other.gameObject == player)
        {
           StartCoroutine(PlatformFalling());
        }
    }
```



## 5. IEnumerator PlatformFalling()

Now we need to create a IEnumerator PlatformFalling() function in which we will actually activate the gravity of the object and after 1 second of falling, the object gets destroyed.
```
 IEnumerator PlatformFalling()
    {
        yield return new WaitForSeconds(FallWaitingTime);
        rb.useGravity = true;
        yield return new WaitForSeconds(1f);
        Destroy(gameObject);
    }
}


## 6. Test

Now you can test if the script works by playing the scene and jumping with the player on the platform.
