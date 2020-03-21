---
title: "djangorestframework(DRF) - basic authentication"
excerpt: "Test level authentication not for production"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-21T08:06:00-05:00
---

## Authentication 

In today's post, we will look through test-level authentication with a get request. Since it uses the get request, the login id and password will be exposed in the URL. It's not a good manner when we build a production-ready service. If you want to see changes in a hurry, please visit the [follow link](https://github.com/devjunhong/django-polls-tutorial/commit/4a68564c196e6e0648919287c85ec6328a13d5ce). 

This post is followed by [this article](https://devjunhong.github.io/django/custom_view_set/).

## Code snippet of using BaseAuthentication 
```python
# polls/api_authentication.py
from django.contrib.auth import authenticate

from rest_framework import authentication
from rest_framework import exceptions as e


class AdminOnlyAuth(authentication.BaseAuthentication):
    def authenticate(self, request):
        try:
            username = request.query_params.get('username')
            password = request.query_params.get('password')
            user = authenticate(username=username, 
            password=password)
        if user is None:
            raise e.AuthenticationFailed('No such user!')
        return (user, None)
    except:
        raise e.AuthenticationFailed('No such user!')
```

The code finds the username and password from the request parameter. If it's possible to login, it will provide a valid result. Here in the authenticate function, it should return authentication with permission for that user. If the user can't valid username or password, simply return the error message. 


```python
# mysite/settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'polls.api_authentication.AdminOnlyAuth',
    )
}
```

If you want to add the authentication feature in the view directly, you can assign using the authentication_classes. The below shows that. So, when we query to question view set, it will check the authentication. 

On the other hand, if we want to make it globally, then please check the above code. Since this is a global setting, it should be in the project-level configuration file. 

```python
# polls/api_views.py
from .api_authentication import AdminOnlyAuth


class QuestionViewSet(viewsets.ModelViewSet):
    authentication_classes = (AdminOnlyAuth,)
    queryset = Question.objects.all().order_by('-pub_date')
    serializer_class = QuestionSerializer
```