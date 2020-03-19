---
title: "DRF custom view set"
excerpt: "djangorestframework, how to create a custom view set?"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-20T08:06:00-05:00
---

## Viewset and APIView

| Viewset                                                               | APIView                                 |
|-----------------------------------------------------------------------|-----------------------------------------|
| Uses DRF defined methods like 'list', 'retrieve', 'create', and so on | Users HTTP Verbs (GET, POST, and so on) |
| Compatible with browsable API                                         | Not compatible with the browsable API   |
| DRF Router compatible                                                 | Cannot use DRF Router                   |

Here are the official document for the [Viewset](https://www.django-rest-framework.org/api-guide/viewsets/) and the [APIView](https://www.django-rest-framework.org/api-guide/views/). In this post, we will take a look at how to implement a custom viewset. 

## Snippet of code for custom viewset
```python
# polls/api_views.py
from rest_framework.response import Response
from rest_framework import viewsets


class CustomQuestionView(viewsets.ViewSet):
    def list(self, request, format=None):
        questions = [question.question_text for question 
        in Question.objects.all()]
        return Response(questions)
```

After we finish up customizing the viewset class, we move to bridge the url. 

```python
# mysite/urls.py
from rest_framework import routers 

from polls import api_views


router = routers.DefaultRouter() 

router.register(r'custom_question', 
api_views.CustomQuestionView, basename='poll')
```

When we check our work, we will get this screenshot. 

![Custom ViewSet](/assets/images/custom_question_list.png)