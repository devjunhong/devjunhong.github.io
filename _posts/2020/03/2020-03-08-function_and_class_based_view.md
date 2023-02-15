---
title: "Function Based View and Class Based View in Django"
excerpt: "Check out the code and feel the difference"
toc: true
toc_sticky: true 

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-08T08:06:00-05:00
---

## List items
```python
from .models import Question


# Function based view
def index(request):
    latest_question_list = Question.objects. \
    order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```

```python
from django.views import generic

from .models import Question


# Class based view
class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        return Question.objects.order_by('-pub_date')[:5]
```

Here is an example of listing items by using 2 different methods. For the function-based view, we need to make sure the call for the 'render' function to pass the result. On the other hand, in the class-based view, we are not sure how to render a page. We have to understand what happens in the class-based view way. Honestly, this can be a hurdle for beginners and also was for me. 


The best way to see the under the hood is by finding parent class code (generic.ListView) in Github since Django is opensource we can check out it. [Link](https://github.com/django/django/blob/9358da704ea9ba55f22df912e47b54eb85d5c97e/django/views/generic/base.py#L30)


## Detail item view
```python
from .models import Question


# Function based view
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', 
    {'question': question})
```

```python
from django.views import generic

from .models import Question


# Class based view
class IndexView(generic.DetailView):
    model = Question
    template_name = 'polls/deatil.html' 
```

In this example, the two codes will serve the page for each item. When we click an item from a page, we would meet the detail description of the item. This will do. 


We can see the function-based view take control for handling the exception but in the class-based view, it seems pretty too simple. 


## Comparison table

| Function Based View     | Class Based view                   |
|-------------------------|------------------------------------|
| More setup              | Little setup                       |
| Less abstraction        | More "MAGIC" abstraction           |
| Requires error checking | Error handling built in (generics) |
| Less modular            | Much more modular                  |
|                         | Sane and Stable generic API        |

This is a summary of what we've seen in the code. Using the function-based view or the class-based view is always up to you. It might be rooted in your preference or size of a project. Here you can find a simple flow chart on how to choose between two. [this post](https://medium.com/@ksarthak4ever/django-class-based-views-vs-function-based-view-e74b47b2e41b).