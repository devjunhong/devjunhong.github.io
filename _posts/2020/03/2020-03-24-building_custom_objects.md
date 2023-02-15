---
title: "Building custom object"
excerpt: "Query customized data"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-24T08:06:00-05:00
---

This post is followed by the [article](https://devjunhong.github.io/django/building_a_basic_graphql_scheme/). It contains examples from the previous article. Please visit the previous article if you can't figure out what's going on here. This is quick [overview](https://github.com/devjunhong/django-polls-tutorial/commit/aebe1a45de2c71ce571df4fa5692da55444cb223) about changes. 


## Types in GraphQL 
* Enums
* NonNull
* List
* Object Types
* Schema
* Mutations 
* Scalars
    * Int
    * String
    * Float
    * Boolean
    * ID
    * Date
    * Datetime
    * Time
    * JSONString
    * Custom Scalar 

This list of types is pretty obvious if we have coding experience. Enum is just like python's Enum class. NotNull means there is no null object and so on. Schema type is the root type for query and mutations. Mutations are a type for modifying server-side data. We can check out the official document for [types](https://graphql.org/graphql-js/type) and [mutations](https://graphql.org/graphql-js/mutations-and-input-types/).


## Code snippet for custom type
```python
# polls/types.py
import graphene


class CustomType(graphene.ObjectType):
    message = graphene.String()
    question_str = graphene.String()
    question = graphene.Field(QuestionType)

    def resolve_question_str(self, info):
        return self.question.__str__()
```


Here is the code how to build a custom type. All resolvers have prefix 'resolve' on the funciton name. In this code, 'questionStr' resolver is defined and it returns question text. 


```python
# polls/schema.py
from .models import Question
from .types import CustomType


class Query(graphene.ObjectType):
    # ...

    def resolve_custom_question(self, info, **kwargs):
        qid = kwargs.get('id')

        cq = CustomType()
        if qid is not None:
            question = Question.objects.get(pk=qid)
            cq.question = question
            cq.message = "Query Succeeded!"
            return cq 
        return None
```

To understand the resolver, I included the query in the below. We want to resolve customQuestion and inside of it, we can nest another resolver. As we can see question resolver is used and choiceSet resolver is nested again. 

```
query {
  customQuestion(id:2){
    message,
    questionStr,
    question {
        questionText,
        pubDate,
        choiceSet{
            id,
            choiceText,
            votes
        }
    }
  }
}
```

If we enter the above query, we will get below result. 

```
{
  "data": {
    "customQuestion": {
      "message": "Query Succeeded!",
      "questionStr": "Do you like Django?",
      "question": {
        "questionText": "Do you like Django?",
        "pubDate": "2020-03-15T13:13:55+00:00",
        "choiceSet": [
          {
            "id": "1",
            "choiceText": "yes",
            "votes": 3
          },
          {
            "id": "2",
            "choiceText": "no",
            "votes": 2
          },
          {
            "id": "3",
            "choiceText": "maybe",
            "votes": 5
          }
        ]
      }
    }
  }
}
```