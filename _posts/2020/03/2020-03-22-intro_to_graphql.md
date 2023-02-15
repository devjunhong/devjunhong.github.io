---
title: "Introduction to GraphQL"
excerpt: "Comparing with REST and graphene"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-22T08:06:00-05:00
---

This post followed by this [article](https://devjunhong.github.io/django/basic_authentication/). It's a series so it contians example from the previous one.


## GraphQL 

GraphQL provides an API interface that users can submit queries to (like SQL) and receive data from. 


```
query {
    allQuestions {
        questionText,
        pubDate
    }
}
```


```
query {
    resolver {
        fields
    }
}
```


The first example shows a practical example and the following is grammar to show what is matching. It means the 'allQuestions' is called a resolver. The two inside of the bracket is called fields. The syntax looks like a JSON. The 'query' is a reserved keyword. This command will return a JSON result with the 'data' attribute. 


```
{
    "data": {
        "allQuestions": [
            {
                "questionText": "Do you like Django?",
                "pubDate": "2020-03-22T07:22:19+00:00"
            }
        ]
    }
}
```


## REST vs GraphQL 

| GraphQL                              | REST                               |
|--------------------------------------|------------------------------------|
| Single API End-Point                 | Little setup                       |
| No Over/Under Fetching Issues        | More "magic" abstraction           |
| Automatically Cascades Relationships | Error handling built in (generics) |
| Extremely Flexible API               | Much more modular                  |
| Building momentum                    | Sane and Stable generic API        |


REST has multiple API end-point. GraphQL does not have multiple end-point. GraphQL does support cascaded relationship for fetching and this bring over or under fetching issues for REST. 

[GraphQL is released at 2015](https://en.wikipedia.org/wiki/GraphQL), 5 years ago but REST API has a much longer history. Building a momentum means the GraphQL has a relatively short history rather than the REST.

To more deep-dive inspection between two, [this article](https://medium.com/@back4apps/graphql-vs-rest-62a3d6c2021d) is a wonderful article full of practical examples. 


## Graphene 
To use graphQL in Django, we will use the [graphene](https://docs.graphene-python.org/projects/django/en/latest/) library. It provides a GraphiQL interface that shows us how to submit a command to fetch and a correspondence result. 