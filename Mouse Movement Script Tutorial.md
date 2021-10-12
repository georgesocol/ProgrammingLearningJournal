# Mouse Movement Script Tutorial

## Description

In this tutorial we will create a script that you can attach to 2D objects in unity so you can move the said object on the screen while on `Play Mode`.

## 1. Create a new scene

Start by creating a new scene.

Add a 2D square, I am going to call it `Square`.

## 2. Add the components

Add a `Rigidbody 2D` and a `Box Collider 2D` to the object with the same component settings as shown in the picture below. 

![Rigidbody 2D and Box Collider 2D settings](https://raw.githubusercontent.com/georgesocol/ProgrammingLearningJournal/main/Pic1.png "Rigidbody 2D and Box Collider 2D settings")

## 3. Create the script

Create a new script named `MouseMovementTutorial` and attach it to the `Square`.

First, we need to add the variables that we are going to use.

```
    public Rigidbody2D selectedObject;
    Vector3 offset;
    Vector3 mousePosition;
```

We will use the `selectedObject` variable to let the script know which object we are going to move when we press on it.

The `offset` variable will be used to make sure that we can "grab" the square from any point on it. If we don't use this variable the object would snap to the center everytime
we will pick it up.

The `mousePosition` variable will let the game know where position of the pointer is in game. This will help the script know if we want touch an object or not, but also to
calculate the `offset` variable value.

## 4. Void Update()

We will start working in the `void Update()` function now.

First we will let `mousePosition` know where exactly on our screen the pointer is.

```
mousePosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
```


After that we will add an `if` statement to test if the left mouse button is clicked and held.

```
if (Input.GetMouseButtonDown(0))
        {
            Collider2D targetObject = Physics2D.OverlapPoint(mousePosition);

            if (targetObject)
            {
                selectedObject = targetObject.transform.gameObject.GetComponent<Rigidbody2D>();
                offset = selectedObject.transform.position - mousePosition;
            }
        }
```

`targetObject`'s value is the object that is under the mouse pointer when we press the left mouse button.

The second `if` statement checks if `targetObject` has an object attached to it or not. When the mouse touches an object, `selectedObject` will get the value of the
`Rigidbody 2D` that the object has.

`offset` will be calculated by substracting the `mousePosition` value from the coordinates stored in `selectedObject.transform.position` that the square has.



After this we will add one more `if` statement to the function.
```
if (Input.GetMouseButtonUp(0) && selectedObject)
        {
            selectedObject = null;

        }
```

This statement removes the value of `selectedObject` when the left mouse button is released.

## 5. Void FixedUpdate()

Now we need to create a `void FixedUpdate()` function in which we will actually move the object.
```
if (selectedObject)
        {
            selectedObject.MovePosition(mousePosition + offset);
        }
```

We add an `if` statement where we check if we have an object that is selected or not in `selectedObject` variable.

If the variable has a value, then the object will be moved following the position the mouse has on the screen. We also add the `offset` variable to the `mousePosition` to let the script know that we can drag the object from any point on the surface of the object.

## 6. Test

Now you can test if the script works by playing the scene and dragging the object around by clicking on it.
