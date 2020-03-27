---
title: "Separating settings files in Django"
excerpt: "Like the Visual Studio Debug and Release"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-27T08:06:00-05:00
---

This post is followed by the [article](https://devjunhong.github.io/django/pipenv_the_new_pip/). To check it out changes, please review this [commit](https://github.com/devjunhong/django-polls-tutorial/commit/acf69a4d7ad5aeb1ae9ac996e4629b122c49fca7).


## Why do we need to separate settings files in Django?

In my case, when I collaborate with other developers, I feel a separation of settings file is required. Let's say I use Mac and a colleague uses Windows. In that case, it is necessary to maintain two settings files. Or, if I want to test it in production mode in Django, then I don't need to set DEBUG but in a development environment. I will turn on the DEBUG setting to find an error. 


## How to separate it? 

1. Create a folder named settings 
```
# at the project directory and the project name is 'mysite'
$ mkdir mysite/settings 
```

2. Move the original settings file and change its name
```
$ mv mysite/settings.py mysite/settings/base.py
```

3. Create a new settings file
```
$ touch mysite/settings/dev_env.py
```

4. Create __init__.py in the settings folder.
```
# This makes the Django recognize the settings folder 
# as a python package. 
$ touch mysite/settings/__init__.py
```

5. Instead of copying all relative settings override required changes. Please checkout [this commit](https://github.com/devjunhong/django-polls-tutorial/commit/acf69a4d7ad5aeb1ae9ac996e4629b122c49fca7). 

6. Execute Django with settings option 
```
# make sure you are in pipenv shell
(pipenv_name) $ python manage.py runserver --settings=mysite.settings.dev_env
```