---
layout: post
title:  "Install an older version of Stack"
summary: "A quick hack to install an older version of the Haskell Tool Stack."
date:   2019-06-17 10:00:00 +0000
comments: true
---
The [Haskell Tool Stack](https://docs.haskellstack.org/en/stable/README/) is a great tool for reliably building Haskell projects. Unfortunately its [latest release](https://github.com/commercialhaskell/stack/releases/tag/v2.1.1) deprecated the `stack image` command, a vital part of my build process. I needed to keep my CI working until I have time to wrangle a replacement for the command, but I couldn't find an easy way to install an older version of Stack.

I ended up using the raw install script from a previous GitHub release just like I would use the script hosted at [https://get.haskellstack.org](https://get.haskellstack.org). The following let me install [Stack 1.9.3](https://github.com/commercialhaskell/stack/releases/tag/v1.9.3):
```
sudo curl -sSL https://raw.githubusercontent.com/commercialhaskell/stack40cf7b37526b86d1676da82167ea8758a854953b/etc/scripts/get-stack.sh | sh &&
```
