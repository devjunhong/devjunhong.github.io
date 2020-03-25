---
title: "Pipenv: The new pip"
excerpt: "Setting up development environment"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-26T08:06:00-05:00
---

In this post, we will walk through about advantages using pipenv. 

## What is the pipenv?

* Written by Kenneth Reitz (Python Software Foundation board member)
* Officially recommended package tool
* Tries to fix the poor and complex tooling of Python
* Uses Pipfiles and Pipfile.lock allowing truly deterministic builds
* Automatically adds/removes dependencies from Pipfile 
* Automatically creates virtual environments

Pipenv is a better tool than other pip or virtualenv tool. This singular tool takes the functionality from both and combines it into one. 

## Commands 

```
$ pipenv install django 
```
The commands install a recent version of Django.

```
$ pipenv install django --dev
```
By using the --dev option, this will install Django in a development environment. 

```
$ pipenv --three
```
This creates an environment with python version 3. 

```
$ pipenv shell
```
We can use this to access the shell created by pipenv. This is what we've seen using the virtualenv. 

```
$ pipenv run python manage.py runserver
```
The above command will execute manage.py one time. It will run the server until we hit the ctrl + c.

```
$ pipenv graph
```
The command creates a nice looking tree to represent all dependencies that can be found in the project. 