---
layout: post
title: "Something a lot like Pokémon Yellow"
summary: "The Pokémon Yellow in my head was something a lot like Pokémon Yellow."
date: 2024-01-02 23:00:00 +0000
image: "/assets/yellow-dalle.png"
---

When I was 7 years I old got my hands on the [Pokémon Yellow Master Guide](https://www.docdroid.net/h24r/nintendo-magazine-1999-pokemon-master-guide-pdf#page=28). I devoured it, leaving it dog-eared from multiple cover-to-cover readings.

![Pokémon guide](/assets/pokemon-guide.png){: width="256" }

But the truth is I didn't even own a Game Boy, yet alone Pokémon Yellow. I prayed against all odds that I'd find a Game Boy on sale for £1 at Poundland, which only went to show that I didn't have a great grasp of economics.

I never got to play Pokémon Yellow. I did, however, have a Pokémon Yellow in my head. From the Master Guide I had gained a surprisingly deep knowledge of the game without ever actually playing it. In my head you could find Moltres on the second floor of Victory Road, just as it is in the real game (I am assured). I didn't know what it felt like to catch Moltres, sure, but I knew its stats, where to find it and what it looked like.

![Victory road](/assets/victory-road.png){: width="256" }

The Master Guide was so comprehensive that you could probably reverse-engineer the whole Pokémon Yellow game from it. Stop a minute to think about what that would look like. Really, what would it look like? It wouldn't be _the_ Pokémon Yellow, but it would be something a lot like Pokémon Yellow. Because of this we will say that the Master Guide is a _good model_ of Pokémon Yellow.

![DALLE-generated image of a Pokémon Yellow screenshot](/assets/yellow-dalle.png){: width="256" }

We could do the same reverse-engineering exercise using a game review. Could we recreate a high fidelity Pokémon Yellow game just from a review? I don't think so. The review would underspecify the game, requiring almost all the details be interpolated. We could create another game that shared similar mechanics, but it wouldn't be much like Pokémon Yellow. Because of this we will say that a game review is a _bad model_ of Pokémon Yellow.

![Pokémon review](/assets/pokemon-review.jpg){: width="512" }

Game guides are good models of games. In 2023 game guides have come a long way, and are now built collaboratively using wikis like [Bulbapedia](https://bulbapedia.bulbagarden.net/wiki/Main_Page). A game wiki is an _excellent_ model of a game. Given a game wiki we should be able to recreate the corresponding game a reasonable level of fidelity.

![Bulbapedia](/assets/bulbapedia.png){: width="512" }

In a normal year this is where the thought experiment would end, but 2024 is not a normal year. With the recent advances in GenAI we now have access to capabilities that were once the reserve of science fiction. Using [text as the universal interface](https://scale.com/blog/text-universal-interface) we can create text, art, audio and code from raw compute. With this technology we could mechanically create a game from just its model. This ceases to be just a thought experiment: we build a system that takes the Pokémon Yellow wiki in and pushes a Pokémon Yellow game out.

Why is this interesting? Suppose we want a new version of Pokémon Yellow with a new Pokémon creature. We don't need to change the game's source code, we just need to edit the wiki and then press the "remake game" button. Modding a game becomes as simple as editing the wiki. Creating a game becomes as simple as writing its wiki.

Despite the GenAI revolution our capabilities aren't yet advanced enough to do this in the general case. However, I believe that today we are already capable of doing this in a restricted environment. I think we could mechanically create a Game Boy era Pokémon game from a model by using a static game engine and dynamically creating the areas, enemies, items etc. from the wiki. It's not easy, but I think it's possible.

This is what I'm hacking on right now: a wiki that makes games. Check out [langengine.com](https://www.langengine.com/waitlist) to join the waitlist.

![Langengine screenshot](/assets/langengine-peek.png){: width="512" }

Some closing thoughts:

- How do we handle the non-determinism of generating parts of the game that are underspecified?
- What happens when we use AI to write the wiki?
- Does this thinking apply outside games?
- How good of a model is Wikipedia for reality?
