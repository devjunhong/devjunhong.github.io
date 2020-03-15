---
title: "Create a custom class based view"
excerpt: "inherite the generic.View class"
toc: true
toc_sticky: true 

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-16T08:06:00-05:00
---

## why generic.View?
* Most basic class based view 
* Defines the fewest methods
* Extremely easy to extend using HTTP Verbs (one or more!)

In this post, we will implement a custom class-based view by inheriting the generic.View class. The parent class for all views in Django. It means the detail view, list view, and others inherit the generic.View class. If we want to build our own view, then this is the first option. We can check out a difference directly with this [link](https://github.com/devjunhong/django-polls-tutorial/commit/9dca05e5d07339d57f3d751699e319cd2beca113). 

## Example - 1
```python
from django.shortcuts import redirect


# class based view, polls/views.py
class VoteView(generic.View):
    def get_queryset(self, choice_id):
        return Choice.objects.get(pk=choice_id) 

    def post(self, request, question_id):
        choice_id = request.POST.get('choice', None) #[1]
        try:
            queryset = self.get_queryset(choice_id) #[2]
        except (KeyError, Choice.DoesNotExist):
            return redirect('polls:detail', 
            pk=question_id) # [3]
        else:
            queryset.votes += 1 # [4]
            queryset.save()
            return redirect('polls:results', pk=question_id) 
```

By inheriting the generic.View class, we can implement a custom class-based view. Instead of the functional-based view, the class-based view is simple and easy. In [1], we can find the 'choice' item from a given post request. On [2], we can check out 'choice_id'. If choice_id does not exist, then [3] redirects to the detail view. If exists, update the value in the [4]. 

## Example - 2
```python
from django.views.generic.base import TemplateResponseMixin 


class ResultsView(TemplateResponseMixin, generic.View):
    template_name = 'polls/results.html'

    def get_queryset(self, question_id):
        return Question.objects.get(pk=question_id)

    def get(self, request, pk):
        queryset = self.get_queryset(pk) 
        context = {'question': queryset}
        return self.render_to_response(context) # [1]
```

Thanks to the TemplateResponseMixin as we can see in the [2], it is possible to call the 'self.render_to_response' and it is the same with the render function. 