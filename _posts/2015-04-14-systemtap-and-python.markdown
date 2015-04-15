---
layout:     post
title:      "Systemtap and python"
subtitle:   "Dynamically tracing python with systemtap"
date:       2015-04-14 20:00:00
author:     "az"
tags:       systemtap python
---

<p>
<h2 class="section-heading">Intro</h2>
Have you ever wanted to see what your python program is doing, live, without placing in annoying print statements. Lets go
even further, you want to see whats happening with the libraries you have imported. Or you wanted to know the path the code
you have written has taken. Luckily systemtap exists. Systemtap allows us to trace applications that have 
predefined probes. Python has the current probe points: 
</p>
<p>
<ul>
<li> entry - probe on entering a function </li>
<li> return - probe on leaving a function </li>
</ul>
</p>

<p>
With the parameters 
<ul>
<li> filename </li>
<li> funcname </li>
<li> lineno </li>
</ul>
</p>

<p>
The probe points exists with the following version of python, shipped with CentOS6
<ul>
<li> python-devel-2.6.6-52.el6.x86_64 </li>
<li> python-2.6.6-52.el6.x86_64 </li>
</ul>
</p>

<p>
<h2 class="section-heading">Examples</h2>
The below example shows a one-liner used to trace a simple hello world python program

{% highlight bash %}
cat -n /tmp/hello.py
     1	#!/usr/bin/python
     2
     3	def hello_main():
     4	   print "Hello world"
     5
     6	def hello_main_two():
     7	   print "Hello Mars"
     8
     9	if __name__ == "__main__":
    10	   hello_main()
    11	   hello_main_two()
{% endhighlight %}
<br>
Now the output:
{% highlight python  %}
sudo stap -e 'probe python.function.entry \
{printf("Filename: %s\nFunction name: %s\n lineno: %d\n\n", filename, funcname, lineno);}' \
-c /tmp/hello.py
Filename: /usr/lib64/python2.6/site.py
Function name: <module>
 lineno: 59
...
...
...
Filename: /tmp/hello.py
Function name: <module>
 lineno: 3

Filename: /tmp/hello.py
Function name: hello_main
 lineno: 3

Filename: /tmp/hello.py
Function name: hello_main_two
 lineno: 6
{% endhighlight %}

We can see the path the python program took in order to complete. Providing us with the filename, path to that file, function name
that was called within that file as well as the line number in chronological order.
<br>
More information can be found here: https://fedoraproject.org/wiki/Features/SystemtapStaticProbes
</p>

<p>
<h2 class="section-heading">In addition</h2>
Kicking off an python application prefixed with the stap command may not be feasiable, what if the application is already running. Systemtap has the ability
to attach to currently running processes

{% highlight python %}
stap -e 'probe python.function.entry \
{printf("EPOC: %d\nFilename: %s\nFunction name: %s\n lineno: %d\n\n", \
gettimeofday_s(), filename, funcname, lineno);}' -x <PID>
{% endhighlight %}

In the above example , as well as attaching to an existing process, we are also printing the EPOC time of when the probe was fired
</p>
