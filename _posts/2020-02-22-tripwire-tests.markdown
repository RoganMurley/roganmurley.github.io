---
layout: post
title:  "Tripwire Tests"
summary: "Tests can be a powerful communication tool."
date:   2020-02-22 10:00:00 +0000
comments: true
---
### Introduction
Tests are usually written to check that code is correct. This is a lofty and noble goal, which makes it easy to forget that they can be used in other ways too. I like to use tests to communicate with future developers who are making certain predictable changes, reminding or warning them through the failure message. I call these tests "tripwire" tests.

### Example: Making sure temporary hacks are temporary
When working on a legacy project I found a bug in the framework we were using. The bug could be worked around with an ugly hack, but it was easy to fix with a PR so I naturally did so. Unfortunately we were stuck on an earlier framework version and not yet ready to upgrade to the latest fixed version. We were stuck with an ugly temporary hack for now.

It seemed excessive to fork the whole framework, but I wanted to make sure the hack would eventually be removed even if I wasn't around to do so. I wrote a tripwire test which failed when the framework was updated to the fixed version. The failure message told the updating developer to remove the hack as it was no longer needed, acting as a kind of forced documentation.

I left the project, the library was upgraded, the tripwire test was tripped and the hack was removed. Happy ending!

### Example: Highlighting when conditions change
I was iterating fast on an admin tool that used the Wikidata API to make a SPARQL query. Conditions were such that I didn't need to worry too much about SPARQL injection: the tool was private and the database was read-only. I did some naive validation of parameters and called it a day, but I was worried about what might happen if these conditions changed. For example, what if we moved from the external read-only database to our own internal read/write database? I added some documentation warning about this but it didn't seem like enough.

I wrote a tripwire test which failed when the value of the API endpoint URL changed, reminding the developer about the security assumptions. Under continuous integration the developer will be forced to acknowledge the warning in a way that just documentation can't do.

### Conclusion
Tests can be a powerful tool for communication. Don't just think of them as testing correctness, consider testing other assumptions as well. I'd love to hear other ways you've used tests to communicate.
