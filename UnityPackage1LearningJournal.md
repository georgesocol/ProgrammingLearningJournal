
# Unity Package 1

I can't access the `Sprites` attached to the images in the `AmmoSystem` script that I am programming. 
The problem was that on the top of the script I wrote `using UnityEditor.UI` instead of `using UnityEngine.UI`.
I was able to access the sprite of the images after the changed the library.

The sprites are changing colors from right to left when using the "bullets". I changed the variable that checks which sprite needs to change in the list.
The new variable that I used is `currentBullet` which gets it's value from `maxAmmo - ammoLeft`. The count will go now from 0 to `maxAmmo`

I couldn't change the amount of bullets shown on the screen, I had a fixed amount of sprites. I added a `Panel` to the canvas, I made the `Bullet` image a prefab and I generated
the `Bullet List` inside the script. In this way it's easier and faster to change the amount of bullets shown on the screen. It's also easier to change the location on the screen,
padding, size and spacing.
