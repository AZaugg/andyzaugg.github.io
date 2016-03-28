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
{% highlight python %}
def security_token():
    uri = 'http://mydomain.my.salesforce.com/services/oauth2/token'
    headers = {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
        'X-PrettyPrint': '1',
    }

    password = "%s%s" % (PASSWORD, APITOKEN)
    payload = {
        'grant_type': 'password',
        'client_id': RF_CONSUMER_KEY,
        'client_secret': RF_CONSUMER_SECRET,
        'username': RF_USERNAME,
        'password': password,
        }

    r = requests.post(uri, verify=True, data=payload, headers=headers)
    r_code = r.json()

    r_code = request_url(HOST, uri, headers, payload)
    access_token = str(r_code.get('access_token'))
    instance_url = str(r_code.get('instance_url'))

    return access_token, instance_url}
{% endhighlight %}
<p>
The payload is important here and is uniq per individual:
<ul>
<li>grant_type - Type of Auth being used</li>
<li>client_id - Is your uniq Remedy force Consumer key from the connected app definition</li>
<li>client_secret - is your uniq Consumer Secret for your remedy force account</li>
<li>username - Your personal username you use to log into remedy force</li>
<li>password - Your personal password concatenated with your personal API token</li>
</ul>

After sending this payload to remedy force, you will receive a similar json response:
</p>
{% highlight json %}
{
  "access_token" : "sfkbnkeufgni23it8gh423pg;bnlsbufisudbg34o87gbjsdbgdhjbdhvka"
  "is_readonly" : "false",
  "signature" : "2bjskuvbelfbaouek",
  "instance_url" : "https://my-domain.my.salesforce.com",
  "id" : "https://test.salesforce.com/id/999990adjbseflb2393fsd",
  "token_type" : "Bearer",
  "issued_at" : "11111111"
}
{% endhighlight}
<p>
From this above response you need to collect the access_token and instance_url.

You will use the access_token in all future requests when hitting the API, and the instance_url will be the endpoint you send all API requests to, which we will demonstrate in Part2
</p>
