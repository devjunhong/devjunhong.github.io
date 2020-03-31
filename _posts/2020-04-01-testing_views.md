---
title: "Testing views in Django"
excerpt: "How to create view test code in Django?"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-04-01T08:06:00-05:00
---

This post is followed by this [post](https://devjunhong.github.io/django/testing_models/). In the previous post, we go through about how to test a model in Django. Please take a look [this commit](https://github.com/devjunhong/django-polls-tutorial/commit/a9d4e30c3320a23f90c6709fffc8117dc17bc14c) if you need to grasp the idea quickly. 


## Testing target code

```python
class VoteView(generic.View):
    def get_queryset(self, choice_id):
        return Choice.objects.get(pk=choice_id) 

    def post(self, request, question_id):
        choice_id = request.POST.get('choice', None) 
        try:
            queryset = self.get_queryset(choice_id)
        except (KeyError, Choice.DoesNotExist):
            return redirect('polls:detail', pk=question_id)
        else:
            queryset.votes += 1
            queryset.save()
            return redirect('polls:vote_results', pk=question_id) 

```

In this post, we will see how to create some test code about this view class. At least, we need to have two test methods; get_queryset and post function. Here in the post method, we have 2 return statements. So, we should develop 3 test cases to cover every line of this view code. 

At first, we need to identify what code needs to be tested like in the above. Besides, we can create more than 3 test cases with edge cases. 

## Snippet of test code 

```python
from django.test import TestCase 
from django.test import RequestFactory 
from django.urls import reverse 

from model_mommy import mommy

from polls.views import VoteView 
from polls.models import Choice 


class TestVoteView(TestCase):
    def setUp(self): 
        self.factory = RequestFactory()
        self.question_model = mommy.make('polls.Question')
        self.choice_models = mommy.make(
            'polls.Choice',
            question=self.question_model,
            _quantity=3
        )

    def test_get_queryset(self):
        choice = self.choice_models[0]
        view = VoteView() 
        queryset = view.get_queryset(choice.pk)
        self.assertEquals(queryset.choice_text, choice.choice_text) 

    def test_post_votes(self):
        choice = self.choice_models[1]
        votes = choice.votes + 1
        request = self.factory.post(
            '/some-fake/url',
            data={'choice': choice.id}
        )
        view = VoteView.as_view()
        response = view(request, question_id=choice.question.id)
        new_votes = Choice.objects.get(pk=choice.id).votes 
        self.assertEquals(votes, new_votes) 

    def test_post_redirects_on_fail(self):
        choice = self.choice_models[2]
        request = self.factory.post(
            '/some-fake/url/',
            data={'choice': 500}
        )
        view = VoteView.as_view() 
        response = view(request, question_id=choice.question.id)
        self.assertEquals(response.status_code, 302) # [1]

```

Since we identify we need 3 test cases, the TestVoteView has 3 test method and one is for initializing. The model mommy help to generate text examples. In [1], we can find the 302 status code. It means that the response fails and it does redirect. Since we make our choice model have 3 quantity, it cannot have the 500 choice index. This makes fool the original code, so it fails to response. 