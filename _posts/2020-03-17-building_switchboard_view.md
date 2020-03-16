---
title: "Building Switchboard View"
excerpt: "When we have hairy messy class based view"
toc: true
toc_sticky: true 

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-16T08:06:00-05:00
---

## Switchboard View 
```python
class SwitchboardView(generic.View):
    def get(self, request, pk):
        view = ResultsView.as_view()
        return view(request, pk)

    def post(self, request, pk):
        view = VoteView.as_view()
        return view(request, pk)
```

When we have two related class-based views, we can combine it into one switchboard view. If we build a messy class-based view, then we might need to manage those class-based views into one switchboard view depending on the type of request just like in the above example. In the example, we divide it into two requests; get and post. It looks like a multiplexer or a gateway to control the request. We can find some changes in the following [link](https://github.com/devjunhong/django-polls-tutorial/commit/9da8c2e93f3dc4a0b850ad5e0574c600e277af45).


## The dispatch method 
```python

class View:
    http_method_names = [u'get', u'post', u'put', 
    u'patch', u'delete',
    u'head', u'options', u'trace'] # [1]

    def dispatch(self, request, *args, **kwargs):
        if request.method.lower() \
        in self.http_method_names: # [2]
            handler = getattr(self, request.method.lower(),
            self.http_method_not_allowed) # [3]
        else:
            handler = self.http_method_not_allowed
        return handler(request, *args, **kwargs) # [4]
```
The dispatch method is called when we use 'View.as_view()' in the urls.py. To understand it, we have to look at what it is. 

At first, what does the 'u' do in front of a string? It represents the encoding type of string and it means Unicode encoding. The detail is [here](https://stackoverflow.com/questions/11279331/what-does-the-u-symbol-mean-in-front-of-string-values). 

The above code is cut out version of the 'generic.View' class. As we can see, [1] is the list of HTTP methods handled by this class. Inside of the dispatch method, [2] checks out the request method name. If it can be handle by this class, a handler will be obtained by [3]. The getattr function finds attribute and back. If there's no attribute, then it will return the 'self.http_method_not_allowed'. Finally, in [4], it returns by calling the handler function.
