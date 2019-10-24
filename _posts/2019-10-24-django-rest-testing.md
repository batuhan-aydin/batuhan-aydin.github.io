---
layout: post
title:  "Django Rest Framework Testing"
date:   2019-10-24 06:20:00 +0700
categories: ['django']
---

Maybe in small projects testing is not important but i think it's one of the must-have skills
that you gotta know. So I was developing a Quora clone, and the first thing i had done was authentication. I'm going to start by writing tests for it.

first we gotta import the modules that we need for testing.

{% highlight ruby %}
from django.urls import reverse
from rest_framework.test import APITestCase
{% endhighlight %}

I will continue writing but first i gotta learn how to format these posts