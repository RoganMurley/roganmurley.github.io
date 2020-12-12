---
layout: post
title:  "Unable to verify the Docker daemon is listening (Digital Ocean / docker-machine)"
summary: "Suddenly can't provision Digital Ocean droplets with docker-machine? Here's a quick fix"
date:   2020-12-12 10:00:00 +0000
comments: true
---
I practice continuous deployment on my side project [GALGA](https://github.com/RoganMurley/GALGAGAME). Every time the [continuous integration pipeline](https://app.circleci.com/pipelines/github/RoganMurley/GALGAGAME?branch=master) finishes green on master the application is deployed... if all goes well. Earlier in the week all deploys broke 😱

Deploying the application involves spinning up a new [Digital Ocean](https://www.digitalocean.com/) droplet using `docker-machine`. Earlier this week every deployment started mysteriously failing with the following error:
```
Error creating machine: Error running provisioning: Unable to verify the Docker daemon is listening: Maximum number of retries (10) exceeded.
```

It turns out that the [latest Docker version doesn't work with `docker-machine`](https://github.com/docker/machine/issues/4858). To make things right again you'll want to pin the Docker engine version like so:

```
--engine-install-url "https://releases.rancher.com/install-docker/19.03.9.sh"
```

It took a while of Googling to find the issue so I'm hoping this post can save someone else the headache.
