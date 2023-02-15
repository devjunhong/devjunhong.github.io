---
title: "Working with mutations"
excerpt: "Update server side data with GraphQL"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-25T08:06:00-05:00
---


This post is followed by previous [article](https://devjunhong.github.io/django/building_custom_objects/). So, it contains examples from that article. To check out quickly, please take a look at this [commit](https://github.com/devjunhong/django-polls-tutorial/commit/a5b07968a5697003ec8fd37cb9d8beb42aecd16f). I build this project gradually so that you can recognize what is changed. 


## What's the mutation? 
As we've covered in the previous [article](https://devjunhong.github.io/django/building_custom_objects/#types-in-graphql), the mutation is a type for updating server-side data. 

| Mutations                                    | Queries                                       |
|----------------------------------------------|-----------------------------------------------|
| Can change data                              | Cannot change data (read-only)                |
| Uses 'mutation {}'                           | Uses 'query {}'                               |
| Pass in arguments through an Arguments class | Pass in arguments through resolver parameters |
| Uses ObjectType to bind resolvers to names   | Uses ObjectType to bind resolvers to names    |

We only see about how to use query. Finding differences between mutation and query makes us understand. The one important is mutations are for changing data. There is a common thing here. Those use ObjectType to bind resolovers to names.


## Custom mutation code
```python
# polls/mutations.py
from django.utils.timezone import now 

import graphene

from .models import Question
from .types import QuestionType 


class CreateQuestion(graphene.Mutation):
    class Arguments: # [1]
        question_text = graphene.String() 

    ok = graphene.Boolean()
    question = graphene.Field(QuestionType)

    def mutate(self, info, question_text):
        question = Question(question_text=question_text,
        pub_date=now()).save()
        ok = True
        return CreateQuestion(question=question,
        ok=ok)


class MyMutations(graphene.ObjectType):
    create_question = CreateQuestion.Field() 
```

At first, we need to define custom mutation by using the above code. As we see in the table, mutation uses the Arguments class and it is for passing arguments([1]). The mutate method must return the mutation object. To finish the definition, we need to wire up using the below code. We defined the MyMutations class and this is for binding the mutation to schema. 

```python
# polls/schema.py
from .mutations import MyMutations

#...

schema = graphene.Schema(query=Query, mutation=MyMutations)
```


## Query example 
```
mutation {
    createQuestion(questionText: "Did this article helpful?"){
        ok
        question{
            id
            questionText
        }
    }
}
```

When we create a question by using the above query, we can see the updates by using the below query. We can see the result in the tail of the array.  

```
query{
  allQuestions{
    questionText
  }
}
```

```
{
  "data": {
    "allQuestions": [
      {
        "questionText": "What's up?"
      },
      {
        "questionText": "Do you like Django?"
      },
      {
        "questionText": "Did this mutation work?"
      },
      {
        "questionText": "Did this article helpful?"
      }
    ]
  }
}
```


## Review Quiz 
* In the GraphQL, what is the data type to change server-side data? 