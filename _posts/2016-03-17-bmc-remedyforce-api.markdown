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

<p>
Using the API was an interesting expierence, so here are some interesting sticking points that I got stuck on:
My language of choice is python, so all examples moving forward will be in python.
</p>

<p>
<h2> Pre reqs </h2>
I am assuming that your useraccount has permission to access the API, and that a remedy force app is already created, your friendly remedy force admin should be able to assist with this. Or try your luck with the following document located [here](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_defining_remote_access_applications.htm)
</p>

<p>
<h2>Authenticating with Remedy Force API</h2>
First step is to get a security access token from the remedy force api, to do this you will need to fire off a request to the API requesting an access token, heres a code snippet that will do this for you:
</p>
