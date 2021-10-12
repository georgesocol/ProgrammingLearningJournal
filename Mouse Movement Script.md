# Mouse Movement Script Journal

### 5/10/2021

I created the Vector 3 called offset to make sure that the object is picked up correctly on the screen, without the offset the object would snap because it was trying
to place the center of the object on the mouse position. With the offset vector the object is picked up in the desired way.

### 12/10/2021
    
I had to put an if variable in the `FixedUpdate` to make sure it's going to pick up the object everytime, even if the game is running slower.

