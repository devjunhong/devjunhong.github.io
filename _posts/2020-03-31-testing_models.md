---
title: "Testing models in Django"
excerpt: "How to create model test code in Django?"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-31T08:06:00-05:00
---

This post is followed by an [article](https://devjunhong.github.io/django/how_django_handles_testing/). Since I use the example project from the last article, you might need to check out what's done in the last article. If you want to see quickly, please use this [commit](https://github.com/devjunhong/django-polls-tutorial/commit/dad7e6a77bb400c23ae6d70dec96e42c1adee3be). 


## Snippet of Testing code 

```python
# polls/test_models.py
from django.test import TestCase 

from model_mommy import mommy 


class TestQuestion(TestCase):
    def setUp(self):
        self.models = mommy.make('polls.Question')

    def test_str(self):
        self.assertEquals(str(self.models), 
        self.models.question_text)

    def test_question_and_date(self):
        self.assertTrue(self.models.question_text in 
        self.models.question_and_date())


class TestChoice(TestCase):
    def setUp(self):
        self.models = mommy.make('polls.Choice')

        def test_str(self):
            self.assertEquals(str(self.models), 
            self.models.choice_text)
```

The setUp method is working like an initializer. So, if we need a member variable, then here is the right place. It will be executed once in every test. In this case, the setUp method will run first then test_str and test_question_and_date will do because those 3 methods are in the same class. 

To run the test, we can use this command. 
```python
$ python manage.py test
```

Each test case has 2 different status; Success or Failure. When we see a fail case, it will report detail information about where we can find the line number. 

There are many types of assertion statements. So, if we need more about the assertions, please visit [this official document](https://docs.djangoproject.com/en/3.0/topics/testing/tools/). 


## Get visualization idea 

```
$ python manage.py 
```
If we follow the above test lines, make sure we have 4 test cases by using the above line. 

```
$ coverage python manage.py test 
```
By using this command, coverage has been updated. 

```
$ coverage html 
```

```
$ python -m http.server 
```

When we check out htmlcov, we will see that our test case effects. 