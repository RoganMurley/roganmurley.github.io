---
layout: post
title:  "Omitting Null Values with Aeson"
date:   2018-02-16 23:56:26 +0000
categories: haskell
comments: true
---
[Aeson](https://hackage.haskell.org/package/aeson) is a powerful Haskell library for encoding and decoding JSON. It wasn't obvious to me how to manually omit `null` values when encoding, so I'm sharing a simple solution below.

{% highlight haskell %}
import Data.Aeson.Types (Pair, Value(Null))

omitNull :: [Pair] -> [Pair]
omitNull = filter ((/= Null) . snd)
{% endhighlight %}

<div id="disqus_thread"></div>
<script>

{% if page.comments %}
/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = {{ page.url }};  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = {{ page.id }}; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
console.log(this);
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://rogan-murley.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}
