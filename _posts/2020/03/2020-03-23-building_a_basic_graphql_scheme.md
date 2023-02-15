---
title: "Building a basic GraphQL scheme"
excerpt: "How to use GraphQL in Django"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-23T08:06:00-05:00
---

This post is followed by an [article](https://devjunhong.github.io/django/intro_to_graphql/). Please take a look at it if you need to and if you need to check in one hand, then please go to this [commit](https://github.com/devjunhong/django-polls-tutorial/commit/73fa8aad60479f805b7e905f08fe4665295a3d2e). Thank you in advance. 


## Install packages
```
pip install graphene graphene-django 
```
To use the GraphQL in Django, we install two packages using pip. 


## Building a scheme
```python
# polls/scheme.py
from graphene_django import DjangoObjectType
import graphene

from .models import Question
from .models import Choice 


class QuestionType(DjangoObjectType):
    class Meta:
        model = Question 


'''
class QuestionType(graphene.ObjectType):
    question_text = graphene.String()
    pub_date = graphene.types.datetime.Datetime() 
'''


class ChoiceType(DjangoObjectType):
    class Meta: 
        model = Choice 


class Query(graphene.ObjectType):
    all_questions = graphene.List(QuestionType)
    question = graphene.Field(QuestionType, id=graphene.Int())

    def resolve_all_questions(self, info):
        return Question.objects.all()

    def resolve_question(self, info, **kwargs):
        qid = kwargs.get('id')

        if qid is not None: 
            return Question.objects.get(pk=qid)
        return None 


schema = graphene.Schema(query=Query)
```

Once we finish setting up the file, we move on to the config setting file and wire the URL. In the Query class, we set all resolvers that will be used in a query statement. The only difference from [the previous example](https://devjunhong.github.io/django/intro_to_graphql/) is using the underbar instead of camel case. Here in the Query class, the members are the resolver name and it's written with an underbar. However, in the GraphQL query statement, we used a camel case. 


## Updates settings 

```python
# mysite/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'polls.apps.PollsConfig',
    'rest_framework',
    'graphene', # add
    'graphene_django', # add
]
# ...
GRAPHENE = {
    'SCHEMA': 'polls.schema.schema'
}
# ...
```


```python
# mysite/urls.py
from graphene_django.views import GraphQLView 


urlpatterns = [
    # ...
    path('graphql', GraphQLView.as_view(graphiql=True)),
    # ...
]

```

After setting up this, since we set True to see graphiql, we will see the graphiql page. 