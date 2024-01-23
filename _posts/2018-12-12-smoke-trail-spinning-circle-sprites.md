## Creating a smoke trail effect with spinning circle sprites

A while ago a saw a really awesome prototype gif from a developer who's work I've come to love: [stuffed wombat](https://twitter.com/wombatstuff)
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">final look &amp; name for the comic game <a href="https://t.co/uc9uYjzWhI">pic.twitter.com/uc9uYjzWhI</a></p>&mdash; Stuffed Wombat (@wombatstuff) <a href="https://twitter.com/wombatstuff/status/978743447548039168?ref_src=twsrc%5Etfw">March 27, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I loved the effect of the seeming alive smoke trails. The way they seemed to move in on themselves in this 1 bit style really appealed to me. In the responses to the tweet someone else picked up on this effect as well and asked about it. The method was so simple and clever its amazing I never thought to do anything like it.

Each part of the smoke "cloud" is just 2 small rotating circles, a white outer circle and a black inner circle. The black inner circle always draws over top of the white outer circles so the white outline gets covered over by other circles when they overlap!

It certainly isn't the most optimized solution but it would suffice for the small nice touch type of effect it is. Additionally I realized this is likely how he handles the textbox overlaps where they seem to join into one textbox as well. Brilliant!

Here's a quick gif of my implementation of this (which took just a few minutes because the effect is so simple):
![Dragging the mouse drops the circles](https://i.imgur.com/4zgPNKW.gif)

For those who want to see source code, [here is a quick and sloppily put together scene I made to work in Nez (FNA).](https://gist.github.com/neipo13/1b7ed5ab83496d73958e51cc951d846a)

Full credit to [@wombatstuff](https://twitter.com/wombatstuff) for this great little effect.