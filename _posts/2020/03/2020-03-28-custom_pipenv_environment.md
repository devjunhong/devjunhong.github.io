---
title: "Custom Pipenv environment"
excerpt: "Build your own environment"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-28T08:06:00-05:00
---

This post is followed by this [posts](https://devjunhong.github.io/django/separating_settings_files/). This post will make it easy to apply the previous post in action. 


## Create .env file 

In our pipenv environment setted-up directory, we can create a file called '.env'. Please make sure you can find Pipfile and Pipfile.lock when you list-up the files in your directory. The file(.env) will be automatically loaded when we enter the shell by this command. 
```
$ pipenv shell
```
We can define environment variables in '.env' file and then use it. For example, if we create a '.env' file and then write the below. 
```
# .env file 
DJANGO_SETTINGS_MODULE=mysite.settings.dev_env
```
After defining a variable, please enter the first command to access the shell. It will show 'mysite.settings.dev_env' when we print out the DJANGO_SETTINGS_MODULE variable. So, when we start our server by using the runserver command, it starts by using the designated settings file. 

Finally, this makes easy to select settings file instead of using the settings flag in the [previous article](https://devjunhong.github.io/django/separating_settings_files/). If we are working with pipenv, then this is the best practice to manage separated settings file. We can keep credentials here since it won't be uploaded into the source control. For more information, please visit [here](https://pipenv.readthedocs.io/en/stable/advanced/#support-for-environment-variables). 