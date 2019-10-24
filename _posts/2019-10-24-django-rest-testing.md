---
layout: post
title:  "Django Rest Framework Testing"
date:   2019-10-24 06:20:00 +0700
categories: ['django']
---

Maybe in small projects testing is not important but i think it's one of the must-have skills
that you gotta know. So I was developing a Quora clone, and the first thing i had done was authentication. I'm going to start by writing tests for it.

First we gotta import the modules that we need for testing.

In accounts.tests.py

{% highlight ruby %}
from django.urls import reverse
from rest_framework.test import APITestCase
{% endhighlight %}

Now we can start writing our tests

{% highlight ruby %}
class UserRegistrationTestCase(APITestCase):
    url = reverse('account:register') #Which url we want to test? account is the app name defined in urls.py, register is the url name

    def test_user_registration(self):
        # testing data
        data = {
            'username':'wolffe',
            'password':'testing1234'
        } 
        # make post request, use url and data arguments
        response = self.client.post(self.url, data, format='json')
        # this simple asks are they equal, if not test fails. If true test is succesful
        self.assertEqual(201, response.status_code)
{% endhighlight %}
