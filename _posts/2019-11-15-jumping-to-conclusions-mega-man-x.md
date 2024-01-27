## Jumping to Conclusions : Mega Man X

Welcome to the first in the `Jumping to Conclusions` series, where I will go back to platformers I loved (and maybe some I didn't) and break down their movement, jumping mechanics, and camera. I was inspired to write this up after trying to explain to [a friend](https://twitter.com/aw0_aj) what worked so well about a certain genre. The game in question wasn't a platformer but it reminded/inspired me to start taking notes when I go back to play some of my favorites or biggest inspirations. These will be mostly aimed at other developers trying to implement a *game feel* like one of their favorites or to spot nice touches in classic games or things that were missing. So let's get started with Mega Man X, one of my all time favorite games!
 
<sub>*SPOILER WARNING*: There will be some minor spoilers to some secret locations in the text & gifs below, but nothing that would ruin the experience in my opinion.</sub>

## Mega Man X
Mega Man X wasn't technically my first Mega Man game, I had Mega Man 3 for DOS, but it *was* the first one I really loved. I never played any of the NES Mega Man games until I was probably a teenager, so I never really got to try the series outside the DOS port (for those that don't know, [the DOS port was *BAD*](https://www.youtube.com/watch?v=eH5uEr5oA_o)). I also never *owned* MMX as a kid, I had just played it over at a friends house and was amazed that the wonky MM3 I played on DOS was in any way associated with this awesome game. Pretty much since that first play session (shoutouts to my elementary school friend Matt) this as been a favorite of mine and really lead to my appreciation of Mega Man in general. 

It's worth noting that in my opinion, MMX tends to be a much less difficult platforming focused game than its predecessors. The character takes up a lot of more of the screen and with the additions of wall jumping and dashing, you can traverse areas in a much more exploratory & combat focused way. There are definitely moments of platforming in the X series, but this first game especially focuses on the exploration allowed by the move from single directional scrolling and "rooms" to this now multi-directional scroll and wide open connected spaces! There is also a good enemy variety and a good number of them to blast away at. I think this notion impacts the way the camera and movement mechanics were implemented.


### The Camera
The MMX camera is actually relatively simple, especially when compared with contemporaries like `Super Mario World` ([a great breakdown of the SMW camera on YouTube here](https://www.youtube.com/watch?v=TCIMPYM0AQg)). Cameras in platformers make a huge impact on the game and often depend on the mechanics, jump heights and relative sprite sizes. Typically platform cameras would 'prefer not to move' and only move when its necessary for the player to continue to see the action. Cameras will also often 'lock' vertically or horizontally or both. MMX follows this tradition but does it in a simple way. Locking vertically and horizontally are both implemented, and following in the vertical axis is done with a basic follow boundaries set up while following on the horizontal axis is much tighter keeping X at the center of the screen when unlocked. 


![side by side jumps](https://imgur.com/0MFAXTa.gif)

<sup>You can see locked (left) vs unlocked (right) vertical axis on two different parts of the same level.</sup>

MMX often plays to its strengths and locks the vertical camera when hitting hallways or other areas where you won't be needing any verticality. It also occasionally has some awkward transitions between the area types depending on what the player did. 

![Camera Transition](https://imgur.com/3MPW3cy.gif)

<sup>Transition between unlocked and locked cameras just after grabbing the dash boots.</sup>

Here we can see the camera making a transition based on your horizontal position, as soon as you hit a certain line, that camera locks slightly higher and falls now go to certain death rather than to a new area (to the right).

The unlocked Y follow camera seems to not have too many additional rules with it - no platform locking that I noticed (check SMW video for more info on platform locking) and no rules about staying locked to bottom or top aside from just following player position. Developers were just smart about floor height placement in areas of transition to keep the camera from going wonky. Looking at it now however I kind of wish there was some platform locking so the camera didn't budge slightly at the peak of the first jump on a new height level but that's a very minor complaint.

As for one of my favorite bits of juice in games, screenshake, MMX does not overdo it. In fact I think the game could use a bit more shake. As it stands the only points which the screen shake stood out were when large bosses & mini bosses jumped up and landed. I would have expected some small shake on X being hit or when bosses are defeated with the large number of explosions but seems to be reserved for just the big ol' robo-boys and as such the screen shake is exclusively vertical as far as I could see.

![Camera Shaking](https://imgur.com/jpv0o2H.gif)

<sup>Dropping the hammer & shaking the screen</sup>

That's basically it when it comes to the camera specifics. Locking in both directions for most boss fights as well as some transition stuff when changing rooms (mostly happens at entrance to boss fights) aside, this is pretty much the only logic the camera has as far as I noticed.

## Movement and the *Jump*
Movement in MMX would be incredibly simple to implement and also works fantastically for this sort of game. There is no acceleration horizontally, movement speed is constant in that direction. You are either moving or you aren't. MMX also implements a dash (😍) and keeps that steady movement speed for that as well. You don't hold momentum out of a dash or have a sudden burst that slows later. You are either moving at dash speed, regular speed, or not moving. It makes the control feel very immediate, especially when contrasted with an momentum heavy game like Sonic or Mario. 

The MMX jump is also relatively simple. It follows a standard arc when the button is held down. Similar to the original Mega Man, you have complete  control while in the air. I noticed no difference in the ability to move or change direction horizontally while in the air vs on the ground. This makes a ton of sense for a game where dodging projectiles and bosses flying around is the main goal vs something like Mario jumping on things is the main challenge. 

![](https://critpoints.files.wordpress.com/2015/05/megaman-jump1.gif)

<sup>An old friend.</sup>


There is also 100% variable jump heights. You can hold the jump button to get up to the max height, or let it go at any point to stop your ascent at exactly that moment. This is *huge* for this game as you often want to drop shots in at an exact height. Max jump height is also just over the height of the character. This contrasts with the, screen-size-relatively smaller, original Mega Man who jumps roughly double his height or Mario who jumps incredibly high. In both of these other games, platforming is more of a direct focus and players are smaller on screen which leads to bigger jumps making sense. The shorter jump height likely also allows for the simplicity of the vertical follow of the camera as it has less change in Y to account for.

MMX also delivers on what I call input buffering (also seen called input caching) which lets you hit the jump button a few frames before landing and still pull off a jump. It seems to lack however coyote time, which lets you jump a few frames after walking off a ledge. If this were a modern game I would expect both to be present, but since the game is not typically all about jumping around and more about blasting away at enemies, it isn't incredibly noticeable, though I did feel it.
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Every platformer should have jump input buffering and coyote time <a href="https://t.co/qE61wIxn6Z">https://t.co/qE61wIxn6Z</a></p>&mdash; Andy (@neipo13) <a href="https://twitter.com/neipo13/status/1183185742018818051?ref_src=twsrc%5Etfw">October 13, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


There are two main things about the jump in MMX that differ from the previous games in the MM series. First is the dash and how the dash affects jumping. Since horizontal speeds are maintained while in the air matching what is on the ground, dashing into a jump allows you to hold that dashed speed for the entire time while you're in the air and also maintains that ability to change direction on a dime and maintain the same speed.

![Imgur](https://imgur.com/QVu6IGE.gif)

<sup>Gotta go fast!</sup>

I think this is *super* important to the feel of the dash since the game is really momentum-less. I can't think of a better way (or even another realistic way) to implement this, have fun dash-to-jump movement and not implement momentum in any way. A game like Celeste has a very different and momentum based dash with the ability to chain dashes and super jump and maintain or gain momentum and it leads to very interesting and fun movement tech, but that is a game with a very different focus. With the goals here being more about that immediacy and the ability to know exactly what is going to happen in the heat of reacting to a boss's attack while also returning fire, having this dash jump that carries over the dash speed from the ground to the air gives that great dash-to-jump feel while also maintaining that feel of complete control all of the time.

The other major difference is the wall jump. Wall jumps allow you to ascend a wall by jumping up it multiple times, you also have the ability to slow your fall by sliding down a wall. The MMX wall jump is slightly different to that seen in games like Meat Boy or Celeste in that the jump up ascent is the main thing the developers expect you to use the wall jump for. Because that is the expected behavior, when you press jump off the wall you are not propelled in the opposite direction very much the way you would be in most platformers wall jumps. The jump only pushes you off the wall a few pixels. It's so slight in fact (and I believe there is some amount of buffer range to how close you must be to the wall to be sliding down it if holding toward the wall) that you can mash the jump button while sliding and trigger the start of the jump animation several times. This seems to have no gameplay implications other than giving us a hint about the way this was implemented.

![Wall jump mashing](https://imgur.com/oKgIAwS.gif)

<sup>Mashing jump while sliding and letting go d-pad as you do it gives some clues as to the wall jump implementation.</sup>

You can also dash jump off of a wall. This does have major implications as it allows you to have that dashed speed while in the air when jumping off a wall. A really nice touch though I wish the buffering on the dash input was a bit longer. It currently requires you to push both buttons at pretty much the same time which can be a bit hard with the default button setup. Dash jumping off the wall is a great addition to a game where many boss fights have climbing the walls to dodge attacks and its a bit disappointing that exact timing is expected for the inputs when the timing can already be tight just reacting to Sting Chameleon smacking you with his tongue.

## How the level design uses these tools
I don't want these posts to be too level design focused as the goal is to help you get the feel of these old games, however I do think that the way game designers designed around these mechanics is an important piece. For example I mentioned before that designers often masked the transition between camera modes by making sure you were on a high enough platform to ensure the camera wouldn't look *off* when making the transition to it's locked height.

Bosses got to have a lot more verticality to their movement and especially a lot more moments where they stay up high. Wall jumping allowed for players to have more to do than just running back and forth and jumping or shooting. The could jump up and hide in a corner or dodge around a grounded foe by wall jumping and dash jumping off the wall. It made times where the enemy was up high less of a "wait for him to land" (outside of Storm Eagle 🙄) and more of a new risk/reward opportunity to get a shot in or dodge an attack. It opened up the boss battles to be much more interesting in my opinion.

The change to the focus on combat also seemed to shorten the levels and make most of them less challenging though. That's not to say the game is easy, but for the most part the levels are kind of a fun romp through a themed level leading up to the challenge in the boss fight. Obviously there are cases where this is flip flopped but for example Armored Armadillo's stage is just a few cool gimmicks (riding on the cart & the chase scene) with mostly vanilla platforming outside those that tend to not be incredibly challenging followed a very difficult boss fight (when you don't have the correct weapon at least). I hope the word gimmick does not come off negatively however, almost every level has a fun set piece type section with Ride Armor, or the aforementioned cart, or a big vertical ascent, sweeping changes based on which bosses were beat previously, etc. I think these keep the levels super engaging even with the shortened more exploration/secret finding and baddie blowing up focus.

## TLDR; Mega Man X Game Feel 
* momentum-less, responsive controls which respond the same in the air as on the ground
* dashing into a jump maintains the dash speed throughout the jump including when you change direction
* jump follows arc (gravity applies as you lift up)
* letting go of jump stops you that frame and you start your descent
* wall jump that only forces you a few pixels away from the wall before returning full control to the player
* basic follow camera
 * tight follow on horizontal
 * looser follow on vertical
* camera lock vertically when in a "hallway"
* screenshake is minor and only goes hard on large boss landings
* short levels with focus on "level gimmick"
* complex boss which takes advantage of new movement
