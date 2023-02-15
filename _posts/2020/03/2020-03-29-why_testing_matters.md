---
title: "Why testing matters?"
excerpt: "Road to build a robust software"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-29T08:06:00-05:00
---


This post is followed by this [article](https://devjunhong.github.io/django/custom_pipenv_environment/). 

## What is Unit Testing? 
"In computer programming, unit testing is a software testing method by which individual units of source code, sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures, are tested to determine whether they are fit for use." by [wikipedia](https://en.wikipedia.org/wiki/Unit_testing).

Unit-test code runs the code that we write and for myself, it can be a manual for other developers. Here is a very simple example of testing code. We can make sure and verify the code runs properly.

```python
from django.test import TestCase 


def add_one(num):
    return num + 1


class VerySimpleTest(TestCase): 
    def test_add_one(self): 
        return_value = add_one(5)
        self.assertTrue(return_value == 6) 
```


## Why Testing? 

| Not Testing                                                | Testing       |
|------------------------------------------------------------|---------------|
| Makes a change                                             | Make a change |
| Starts runserver                                           | Write Tests   |
| Opens tab/browser to the right URL                         | Run Tests     |
| Navigates to the page the code is used on (through logins) |               |
| Manually tests the usage of the code                       |               |
| Manually tests every edge case                             |               |

The first column shows when we don't have testing in our workflow. I think manual testings can bring human error which is inevitable and it consumes our time. On the other hand, in the case of including testing in our workflow, we can simply type our testing code and run them. When we update our code, we can find side-effects that probably make bugs. 

* Allows yourself and others to make sure your change doesn't break other changes
* Work as documentation for others to see what your code is supposed to do
* Help sort out edge cases
* Improves onboarding time 


## More resources on Testing 
* [Resons for not writing unit tests](https://tommcfarlin.com/not-writing-unit-tests/)
* [Test-Driven Development with Python - book ](https://www.obeythetestinggoat.com/)
* [Any good arguments for not writing unit tests?](https://stackoverflow.com/questions/2933391/any-good-arguments-for-not-writing-unit-tests)