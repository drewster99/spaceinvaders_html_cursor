## A quick implementation of a classic "Space Invaders" style game in HTML + Javascript + CSS, build using the Cursor.AI LLM-based IDE.
You can [play it here](https://nuclearcyborg.com/ai/spaceinvaders/).

![spaceinvaders-screenshot](https://github.com/user-attachments/assets/f9ea1ba0-f979-428a-af2d-f789960c43ae)

### Implementation
*This was implemented entirely by telling Cursor.AI what I wanted, and took somewhere between 60 and 90 minutes to get what you see here.
While this is still rough around the edges, it's pretty impressive to me here on the last day of 2024 for being a thing where I didn't write a single line of code.*

### Trouble with Blockades
The most difficult part was getting it to handle bullets hitting the little blockades correctly.  It kept wanting to just delete a random pixel out of the blockades when they were hit by the bullet, rather than deleting a chunk that made sense.

Once the blockades were finally working, I had told it to make the enemies in level 2 in the form of a rectangle.  It made something rectangle-ish, with the bottom row spaced down too far, and one of the upper corners not quite aligned.  Not sure what was up with that, but then I told it this:

> that's pretty good. the enemies on level 2 aren't quite in a rectangle.  please fix that.  set up arrangements of enemies in each level as follows:
> 
> level 1: as-is -- do not change this.
> level 2: enemies in a rectangle formation
> level 3: enemies in 2 separate square formations
> level 4: enemies in a heart formation
> level 5: enemies in a grid like in level 1, except that the top row of enemies should be colored red, and they should shoot 3 times as often as the regular enemies.  in addition, their bullets should also be red.  if the player is hit by a red bullet, the player should flash red.
> 
> again do your best work.  when you are ready to generate output, review the generated output and fix any mistakes or bugs first

### More Trouble

This got us **almost** to the game you see now, though there was one more bug where the blockades could not be entirely destroyed.  This was because the game was hit testing against all the blockade sections, including the "hidden" chunks which had been already removed.  As a result, bullets couldn't penetrate past the outer-most layer.
One more bit of prompting got that fixed:

> the code for checking blockade collisions isn't right.  from the behavior, it seems it's comparing against all the blockade pieces rather than just the visible ones.  as a result, the bullets won't completely destroy the blockade.  please fix.
