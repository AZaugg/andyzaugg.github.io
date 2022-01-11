---
layout:     post
title:      "My first post1"
subtitle:   "Lets try out github pages"
date:       2015-03-21 16:00:00
author:     "az"
tags:       examples
---
My first post.

<p>Lets give github pages a try, using jekyll and a nice looking template startbootstrap-clean-blog-jekyll:
<ul>
   <li>https://pages.github.com/</li>
   <li>http://jekyllrb.com/</li>
   <li>https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll</li>
</ul></p>

<h2 class="section-heading">Code blocks</h2>
<p>
Lets try using "syntax highlighting"
{% highlight python linenos %}
worlds = ["Earth", "Mars", "Jupiter"]
for world in worlds:
   print "Hello %s" % world
{% endhighlight %}
</p>


<h2 class="section-heading">Quotes</h2>
<p>
Whats about quoteing things
<blockquote>repeat or copy out (words from a text or speech written or spoken by another person).</blockquote>
</p>

test

break

{{ site.github.project_title }}

contributors

{% for contributors in site.github.contributors %}
  * [{{ contributors.login }}]({{contributors.contributors_url}})
{% endfor %}

Releases1

{% for release in site.github.releases %}
  * [{{ release.url }}]
{% endfor %}


{{ site.github.latest_release.name }}
    
    
    
    

