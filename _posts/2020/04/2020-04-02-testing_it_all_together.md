---
title: "Testing it all together"
excerpt: "Integrate testing in Django"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-04-02T08:06:00-05:00
---

This post is followed by this [article](https://devjunhong.github.io/django/testing_views/). If you want to take a look at GitHub commit, then please visit [here](https://github.com/devjunhong/django-polls-tutorial/commit/cde116a522bd5153ca7e41356a9f0dccf3ed4694). 


## Integration testing in Django 

What we want to do here is creating test cases for mimicking a web browser works; sending a post request with test code. We want to develop a test case in our example. In our example, we can make a post request to API service by selecting a choice from each question. So, we create a test code for that case. 


## Snippet of test code 

```python
from django.test import TestCase 
from django.test import Client # [1]
from django.urls import reverse # [2]

from model_mommy import mommy 


class TestVoteViewIntegration(TestCase):
    def setUp(self):
        self.client = Client() 
        self.question_model = mommy.make('polls.Question')
        self.choice_models = mommy.make(
            'polls.Choice',
            question=self.question_model,
            _quantity=3
        )

    def test_post_success(self):
        choice = self.choice_models[0]
        response = self.client.post(
            reverse(
                'polls:vote_results',
                kwargs={'pk': choice.question.id}
            ),
            {'choice': choice.id},
            follow=True
        )
        self.assertIn(302, response.redirect_chain[0])
        self.assertTemplateUsed(response, 'polls/results.html')

    def test_post_failure(self):
        choice = self.choice_models[0]
        response = self.client.post(
            reverse(
                'polls:vote_results',
                kwargs={'pk': choice.question.id}
            ),
            follow=True
        )
        self.assertIn(302, response.redirect_chain[0])
        self.assertTemplateUsed(response, 'polls/detail.html')
```

To create a test case, there will be 2 scenarios; success or failure. We create 2 test methods. The Client [1] from django.test work as a web browser. It can send requests and back. The reverse [2] helps us to determine the actual URL by string arguments. The string tag will be designated on the 'urls.py' file. 