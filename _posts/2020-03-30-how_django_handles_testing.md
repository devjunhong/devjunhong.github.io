---
title: "How Django handles testing?"
excerpt: "Create test code for Django project"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-30T08:06:00-05:00
---


This post is followed by this [post](https://devjunhong.github.io/django/why_testing_matters/). 


## Useful tools 

* Model Mommy - Generates models with random information so that you don't have to worry about fixtures
* Coverage.py - Shows what you're testing and what you missed

For fluently running our test, we need to generate data and it is time-consuming. So, the Model Mommy package takes over the task to generate random data. It's not human-readable but it's enough to quickly use in our testing. It seems model mommy is renamed as a model bakery. We should use [model bakery](https://model-bakery.readthedocs.io/en/latest/) in the future. 

![Ussage of Model Mommy](/assets/images/model_mommy_in_shell.png)

In the figure, we can find a model created by model mommy with randomly filled. Model mommy can find the model by a string name and it can create a foreign key relationship too. There are two models of question and choice. Question and choice have a foreign key relationship and we can observe the model mommy generate it.


## Build testing environment 

1. Choose an app that we want to test 
2. Create tests folder while removing tests.py 
3. Create '__init__.py' file to be recognized as a python package 

To have a benefit from the coverage package, we need to config about it. 

1. Create .coveragerc in the main project directory
```
[run]
source = .
```
Without this file, the coverage package will inspect the whole python directory and it's not what we want. 


## Visualize view 

To get a nice visualized view of our testing, we can type.
```
$ coverage html 
```
This will create a htmlcov directory and then when we run a local server. 
```
$ python -m http.server
```
Now, we run a simple server based on this directory and now check out the web browser. 

![Coverage creates this list](/assets/images/htmlcov.png)

![polls views coverage](/assets/images/polls_views.png)

These give us a lot of ideas about what needs to be tested and skipped. Since the Django project is shipped with default testing such as checking the type and default route, it covered pretty much of the simple project. 