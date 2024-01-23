## Storing Flags with Bitwise Operators!

Sometimes games just have a lot of flags. Flags for which collision layers a collision box is active on or collides against, flags for events in game that have completed (or not), or flags for just about anything! When I say flags, all I mean is a variable that holds a binary true or false option. We use these all over the place as programmers.

For me the most common use of flags is for collision layers. Nez (my engine of choice) uses an integer as the type for its `Collider.physicsLayer` and `Collider.collidesWithLayers` variables which means I _no choice_ but to use flags. And honestly I'm quite happy it does this. It lets me simply define a bunch of physics layers like this:
```csharp
public static class PhysicsLayers
{
    public const int tiles = 1 << 0;             //binary 0001
    public const int move = 1 << 1;              //binary 0010
    public const int switchActivation = 1 << 2;  //binary 0100
    public const int inspectActivation = 1 << 3; //binary 1000
}
```
and then assign them easily like this:
```csharp
//this collides with both switch and inspect layers
activatorBoxCollider.collidesWithLayers = switchActivation | inspectActivation;
```

## The Symbols.. What do they mean?

The above code has some bitwise operators which are important to understand in this context. The `<<` is a bit shift, which combined with a leading 1, ends up giving powers of 2 (which is what we need here). This bit of code could easily look like:
```csharp
public static class PhysicsLayers
{
    public const int tiles = 1;             //binary 0001
    public const int move = 2;              //binary 0010
    public const int switchActivation = 4;  //binary 0100
    public const int inspectActivation = 8; //binary 1000
}
```
and it would still work the exact same. I use the bit shifters so I don't have to calculate powers of 2 (however easy that might be) and hardcode that. It would also let me use enums if I wanted to go that route. You can see the binary on the right where the 1 shifts to the left (`<<`) by 1 more each time.

Then comes the `|` operator: this is the _bitwise OR_ which essentially joins the bytes of two numbers (`0110 | 0011 = 0111`) as it takes 1 in that bit slot if either of the numbers has a 1 there or 0 otherwise).In our case because we are doing powers of 2, each of these will have only one byte set to 1 and the rest 0 which makes the bitwise OR incredibly simple (and useful)!

Once we have OR'ed together some power of 2 numbers, we can check for any of them by using the bitwise AND operator (`&`) to check for its existence: 
```csharp
//checks !=0 (if the layer is not there this returns 0, otherwise it returns switchActivation)
bool hasSwitch = (activatorBoxCollider.CollidesWithLayers & switchActivation) != 0;
```
The `&` operator does the same thing as the `|` *except* both the left and right numbers must contain a 1 in that bit for it to be passed to the result (`0110 & 0011 = 0010` to continue the example from above) In this way, if we included `switchActivation` in the bitwise OR'ed statement creating `activatorBoxCollider.CollidesWithLayers` then this would return true! A great way to store these.

## What else can you do with this?
Glad you asked! Recently a friend in Discord was talking about saving a large number of flags related to unlocked items. The most efficient way to do so would be with these bit flags again!

```csharp
//an integer to hold the combined bools
int flags = 0;
		
// loop over each bool (order matters here)
for(int i = 0; i < boolsToSave.Length; i++)
{
	//bit shift 1 << number of loop to plant into the int
	if(boolsToSave[i])
	{
		// the | joins the two and the bitshifted 1 acts as a 2 to the power of i)
		// in english the (1 << i) just lets i be identifier of the bit in the int
		flags = flags | (1 << i);
	}
}
```

Then to pull the bools back out (in the same order):
```csharp
// then to convert back to bools
for(int i = 0; i < boolsToLoad.Length; i++)
{
	boolsToLoad[i] = (flags & (1 << i)) > 0;
}
```

This way your save files just need to store an integer instead of up to 32 boolean flags!
(full code stored in this .netfiddle - https://dotnetfiddle.net/qe5Iv5)

## I still don't get it
That's okay! Wrapping your head around bitwise operations takes a bit of getting used to. I will likely do a less game specific, ultra simplified version describing bitwise operations as my next post and will update here. In the meantime there are a few articles on google (most of which look way too intimidating but you can do it!) that you can check out.