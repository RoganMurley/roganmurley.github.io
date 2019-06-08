---
layout: post
title:  "The bug I wish I hadn't caught"
image: "/assets/catherine32_playing.png"
summary: "I'm usually glad to catch a bug before release, but not this time."
date:   2019-06-08 10:00:00 +0000
comments: true
---
When I catch a bug before release I'm usually glad, because I've narrowly averted ruining someone's experience or eating their data. Today I found a bug that I wish I hadn't caught, a bug that I wish I'd released into the wild to witness in its full glory. I found this bug in my digital card game [Ring of Worlds](https://github.com/RoganMurley/Ring-of-Worlds), and I'll tell you its story.

The diligent player `Catherine32` has been grinding the `CPU` player for experience points. She's making good progress but not enough; she wants more, much more. She wonders how much experience `CPU` must have, playing against her and everyone else with no rest. It must be quite a lot.

![Catherine32 playing](/assets/catherine32_playing.png)

`Catherine32` tries to look up the `CPU` stats but finds something mysterious... there is no `CPU` account! It doesn't have an account because it's not a real player, so all of its experience goes into the void. It plays so many games but doesn't get any experience. Tough break.

Late that night `Catherine32` gets a mischievous idea. She opens up her computer and creates an account. That account's name? `CPU`. She does literally nothing for the next 7 days. The `CPU` account does the opposite of nothing, eating up experience through all hours via its robot slave. It becomes a behemoth, leveled above all others. Yet it is still under the control of `Catherine32`, and she is on top of the world.

Oops, it turns out players are looked up by username even if they're an AI with no account. You can harvest the AI's experience just by creating an account with the same username. This is a silly artefact left over from when there were no real player accounts and everything was just drop-in-drop-out.

![SQL statement showing that the CPU player has lots of experience](/assets/cpu_experience.png)

All the players hide in fear, for nobody can hope to match the experience of the dreaded `CPU`. Until one day a new challenger arises, an account named `Guest`. It turns people play a lot of games when not signed in too. `CPU` and `Guest` become locked in an eternal war for experience supremacy, at least until I ban them both.

Unfortunately this didn't actually occur because I caught the bug before release, but I wish it did. In fact, I was very tempted to just close my eyes and pretend I hadn't seen anything. If you fancy hoarding some sweet experience yourself then [sign up and play](https://www.ringofworlds.com/signup)!

<div id="disqus_thread"></div>
