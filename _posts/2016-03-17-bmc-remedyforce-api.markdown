---
layout:     post
title:      "BMC Remedy force and its API - Part 1"
subtitle:   "Auth"
date:       2016-03-17 18:00:00
author:     "az"
tags:       api remedyforce python
---
<p>
I currently work in an environment that is using the [ITIL](https://en.wikipedia.org/wiki/ITIL) framework. So raising change requests are a necessary evil that must be done when change is happening within the environment.  Unfortunately this doesn't work well with continuous and scheduled changes that occur and the idea of standing changes do not currently exist. The tool that I need to use is Remedy force, luckily they provide us with a API as raising the same changes week after week becomes extreamly tedious.
</p>
