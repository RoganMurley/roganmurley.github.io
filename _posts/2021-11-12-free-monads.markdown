---
layout: post
title: "Game rules with a Free Monad DSL"
summary: "How and why GALGA uses a Free Monad DSL for its game rules."
date:   2021-12-11 13:00:00 +0000
comments: true
---
This post is about how and why my multiplayer card game [GALGA](https://www.galgagame.com) uses a Free Monad DSL for its game rules. If that's gobbledygook to you, read on and hopefully it'll make at least a little more sense by the end!

![GALGA gif](/assets/galga2.gif)

[GALGA](https://www.galgagame.com) is like Magic: The Gathering in that each card has its own special rules that change the game. These rules can be simple, like "heal 10 life", or more complex, like "make healing deal damage instead".

The rules are a [Domain-Specific Language](https://en.wikipedia.org/wiki/Domain-specific_language) (DSL) for describing what happens in the game. They are like a mini programming language that runs only on the machinery of the game. Interestingly (or perhaps frighteningly) rules can rewrite other rules at runtime. The rule "make healing deal damage instead" rewrites healing rules to damage rules. The rules DSL can actually **metaprogram itself**!

I implemented [GALGA](https://www.galgagame.com/) in Haskell, and one of the many motivations for this is that Haskell has great support for embedded DSLs. It lets you write a DSL while retaining the full and considerable power of the Haskell type system. It shouldn't be surprising that a language steered by programming language researchers would be good at writing programming languages 😉

There are a few different ways to use embedded DSLs in Haskell ([Free Monads](https://www.haskellforall.com/2012/06/you-could-have-invented-free-monads.html), [Tagless Final](https://serokell.io/blog/introduction-tagless-final) and more). Free Monads are *usually* the wrong choice as they are worse than the other options in both performance and type complexity, but I chose to use them anyway for reasons I'll be digging into below.

![Another GALGA gif](/assets/galga.gif)

***A note for the non-Haskeller: the word "monad" might have scared you off there! If you don't have a vague understanding of monads, I wouldn't recommend looking for an explanation online. Rather, the only way to truly understand them is to get stuck into Haskell and experience the problems that monads try to solve. There is no other way!***


So what is a "free" monad?


Free as in freedom?


Free as in beer?


No, [_mathematically_ free](https://en.wikipedia.org/wiki/Free_object).


A free monad is a monad that satisfies the monad laws and nothing more. It has all the stucture of a monad and none of the "effects". I like to think of it as a program AST ([Abstract Syntax Tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree)) without an interpreter. The free monad represents some computation, but it doesn't define what that computation actually means until paired with an interpreter. Different interpreters can interpret in different ways.

Other flavours of DSL can swap implementations in much the same way free monads swap out interpreters, so why choose free monads? Their unique edge is that the "AST" is maintained and can be introspected and metaprogrammed. Earlier I mentioned that this is a key requirement of our DSL, because we have cards that rewrite the rules of other cards at runtime.

*(side note: "freer" monads improve on the performance and interpreter composability of free monads, but I haven't looked deeply into them yet)*

![GALGA gif](/assets/galga3.gif)

GALGA implements multiple embedded DSLs using free monads. There is a high level DSL for game rules as discussed, and lower level DSLs for changing state directly and visualization. The rules DSL interprets to the lower level DSLs as needed, usually embedded together.

The [primitive DSL](https://github.com/RoganMurley/GALGAGAME/tree/89064b75f92250c5ce327e261f1ad76eea600c25/server/src/DSL/Alpha) is a low level DSL for changing the game state, consisting of only basic getters and setters. When interpreted it mutates the game state. I like to think of it as the "machine code" to which the rules DSL compiles.

```haskell
-- Example primitive DSL program
do
  let which = PlayerA
  life <- getLife (other which)
  setLife (other which) (life - 4)
```

The [animation DSL](https://github.com/RoganMurley/GALGAGAME/tree/89064b75f92250c5ce327e261f1ad76eea600c25/server/src/DSL/Anim) is a low level DSL for visualization. When interpreted it calculates state diffs and associated animations to send to players. Because it relies on accessing the game state it is only interpreted when embedded with the primitive DSL.

```haskell
-- Example anim DSL program
Anim.hurt PlayerB 4 Slash
```

The [rules DSL](https://github.com/RoganMurley/GALGAGAME/tree/89064b75f92250c5ce327e261f1ad76eea600c25/server/src/DSL/Beta) is the high level DSL for describing the game rules, things like drawing cards or healing. When interpreted it compiles to the primitive and animation DSLs embedded together.

```haskell
-- Example rules DSL program
do
  let which = PlayerA
  hurt 4 (other which) Slash
  draw which which 1
```

Because Haskell is a lazy language we only compute the interpretations of the rules DSL that we actually use. In some case we only need the state change, for example when the [AI evaluates moves](https://github.com/RoganMurley/GALGAGAME/blob/0f119962d4e6a240ee549b9d1134bbbcc807030b/server/src/ArtificialIntelligence.hs#L43). If we simply don't use the animations they are never computed.

Because Free Monads give us ASTs for our DSLs, we can metaprogram them by transforming those ASTs. For example, the rule "healing deals damage instead" can be implemented as a [rewrite rule that replaces healing AST nodes with damage nodes](https://github.com/RoganMurley/GALGAGAME/blob/0f119962d4e6a240ee549b9d1134bbbcc807030b/server/src/StatusEff.hs#L29). This is why we have a separate DSL for rules rather than making it an abstraction over the primitive DSL. It is impossible to identify healing to damage when the AST nodes are just getters and setters.

```haskell
-- Example healing to hurting rewrite rule
rewriteRule :: Rules.DSL a -> Rules.DSL a
rewriteRule (Heal l w n) = Hurt l w Curse n
rewriteRule dsl = dsl
```

Embedded DSLs have proved a powerful pattern. I initially planned to use the DSLs only for card rules, but they have expanded to be used for every part of the core game logic. They are the killer feature of Haskell and I will definitely be using them again in the future. As for free monads, I wouldn't recommend them for most use cases as they are relatively complex and slow compared to alternatives. However, metaprogramming was crucial for this project and so they were the right choice.

I hope you gleaned something useful from this blog post! If you did, consider checking out [GALGA for free in your browser](https://www.galgagame.com), or [peruse the source on GitHub](https://github.com/RoganMurley/galgagame) 🙇‍♂️

*May your wheel keep turning.*
