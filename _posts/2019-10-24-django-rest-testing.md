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

Now we can start writing our tests. First we gotta think every possibility write tests for it

{% highlight ruby %}
class UserRegistrationTestCase(APITestCase):
    # Succesful registration
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

        def test_user_invalid_password(self):
        data = {
            'username':'wolffe',
            'password':'1'
        }
        response = self.client.post(self.url, data, format='json')
        self.assertEqual(400, response.status_code)

    def test_unique_name(self):
    # What if username was not unique
        self.test_user_registration()
        data = {
            'username':'wolffe',
            'password':'testing4321'
        }
        response = self.client.post(self.url, data, format='json')
        self.assertEqual(400, response.status_code)    

    def test_user_authenticated_registration(self):
    # What if a user logined by sessions
       self.test_user_registration()
       self.client.login(username="wolffe", password="testing1234")
       response = self.client.get(self.url)  
       self.assertEqual(405, response.status_code)

    def test_user_authenticated_token_registration(self):
    # What if user logined by jwt auth, still tries to register
       self.test_user_registration()
       data = {
            'username':'wolffe',
            'password':'testing1234'
            }
       response = self.client.post(self.url_login, data, format='json')  
       self.assertEqual(200, response.status_code)
       token = response.data['access']
       self.client.credentials(HTTP_AUTHORIZATION = 'Bearer ' + token)
       response_2 = self.client.get(self.url)
       self.assertEqual(403, response_2.status_code)      
{% endhighlight %}
