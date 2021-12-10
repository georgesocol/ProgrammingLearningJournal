# Moving Player With an Object Tutorial

## Description

In this tutorial we will learn how to make the player "stick" with an object, so if the object moves, the player will move along without any keyboard input.

## 1. Create the object that will move

I created a cross that will spin continiously.
I attached a collider to it so the player can "sit" on the cross.

## 2. Understanding the problem

The player can sit on the object, but if the object is spinning, the player would fall after a short time because it doesn't move along with the object.

## 3. Creating the script

We will add the cross to an `Empty GameObject` and we will add a trigger on the parent.

Then we will create a script that we will attach to the empty object. The script is really short and easy to understand, but it could be really useful in a lot of situations.

I called the script `ParentChange`.

```
    public GameObject player;

    private void OnTriggerEnter(Collider other)
    {
        if (other.gameObject == player)
        {
            player.transform.parent = transform;
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.gameObject == player)
        {
            player.transform.parent = null;
        }
    }
 ```
 When the player enters the trigger, the player will become the child of the `Empty GameObject`, exactly as the cross is.
 
 Because the player and the cross are both children of the same object, they will move together, so the player won't fall anymore from the cross.
 
 When the player exits the trigger, it will become once again a single object, without any parent.
 
 ## 4. Testing
 
 After all the steps are done, everything should be working perfectly. The script could be used in a lot of ways, especially where you have moving platforms or the player needs to move along with an object.
 
