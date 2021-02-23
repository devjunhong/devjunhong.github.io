---
title: "Read error message carefully Python"
excerpt: "Reading the full error message is the beginning step of debugging."
# toc: true
# toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/02/24/error_message.jpg
  # image: /assets/images/2021/02/06/soft_skills_v2.jpeg
  caption: "Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/404-error?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)"
  
  # og_image: /assets/images/2021/02/06/soft_skills_v2.jpeg
layout: single
classes: wide
word-wrap: break-word;
categories:
    - Python
tags:
    - Python
last_modified_at: 2021-02-24T08:06:00-05:00
---

Yesterday, I tried to install a python package in a conda environment. I got this message. 

```text
ERROR: Command errored out with exit status 1:
```

I've searched with this statement and there are several trials to beat this error; upgrading pip or upgrading setuptools. Nothing worked. Then, I realized that I've read a small part of the full error message. Okay, go through it. 


```text
ERROR: Command errored out with exit status 1:
  command: /home/username/anaconda3/envs/preprocess/bin/python -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-req-build-vtqxcvpj/setup.py'"'"'; __file__='"'"'/tmp/pip-req-build-vtqxcvpj/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base /tmp/pip-pip-egg-info-gipoehix
      cwd: /tmp/pip-req-build-vtqxcvpj/
Complete output (13 lines):
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/tmp/pip-req-build-vtqxcvpj/setup.py", line 102, in <module>
    'matplotlib'
  File "/home/username/anaconda3/envs/preprocess/lib/python3.6/site-packages/setuptools/__init__.py", line 152, in setup
    _install_setup_requires(attrs)
  File "/home/username/anaconda3/envs/preprocess/lib/python3.6/site-packages/setuptools/__init__.py", line 147, in _install_setup_requires
    dist.fetch_build_eggs(dist.setup_requires)
  File "/home/username/anaconda3/envs/preprocess/lib/python3.6/site-packages/setuptools/dist.py", line 689, in fetch_build_eggs
    replace_conflicting=True,
  File "/home/username/anaconda3/envs/preprocess/lib/python3.6/site-packages/pkg_resources/__init__.py", line 777, in resolve
    raise VersionConflict(dist, req).with_context(dependent_req)
pkg_resources.ContextualVersionConflict: (idna 3.1 (/tmp/pip-req-build-vtqxcvpj/.eggs/idna-3.1-py3.6.egg), Requirement.parse('idna<3,>=2.5'), {'requests'})
----------------------------------------
```

This is the full error message. I'm confused about the front part of the message but the big hint I've noticed that there is a version conflict of "idna" package. I mean the last part of the error message. 

```text
pkg_resources.ContextualVersionConflict: (idna 3.1 (/tmp/pip-req-build-vtqxcvpj/.eggs/idna-3.1-py3.6.egg), Requirement.parse('idna<3,>=2.5'), {'requests'})
```

Gotcha, after I reinstall the "idna" package version 2.7, the desired package was installed correctly. I need to read all the error messages carefully and figure out what I need exactly. By the way, I think Python needs a way more advanced package manager for each project. Please let me know if you know some of it. I know the "requirements.txt" does exist but it sometimes has a dependency issue. So that I don't need to constantly run the script until it has no dependency problem. 