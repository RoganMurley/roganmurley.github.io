---
layout: post
title:  "Omitting Null Values with Aeson"
date:   2018-02-16 23:56:26 +0000
categories: haskell aeson
---
[Aeson](https://hackage.haskell.org/package/aeson) is a powerful Haskell library for encoding and decoding JSON. It wasn't obvious to me how to manually omit `null` values when encoding, so I'm sharing a simple solution below.

{% highlight haskell %}
import Data.Aeson.Types (Pair, Value(Null))

omitNull :: [Pair] -> [Pair]
omitNull = filter ((/= Null) . snd)
{% endhighlight %}
