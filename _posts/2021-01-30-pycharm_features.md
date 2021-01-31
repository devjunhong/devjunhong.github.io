---
title: "Remote debugging and Productivity guide in Pycharm"
excerpt: "Save hundread of my days"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/30/py_prod_guide.png
#   image: /assets/images/2021/01/24/openface_og_updated.png
#   caption: "Photo by me"
  og_image: /assets/images/2021/01/30/py_prod_guide.png
layout: single
# classes: wide

categories:
    - Python
tags:
    - Pycharm
last_modified_at: 2021-01-30T08:06:00-05:00
---

# Intro 
How can we create a program faster? Do you need to boost your productivity? I'm trying to track my productivity and boost it up. What can be the easiest way to achieve it? I can say getting used to study features of your favorite IDE. Using shortcuts save your time instead of touching the mouse. (It maybe very little, but think about when it's accumulated) Yes, I'm talking about few seconds to access the mouse. Honestly, when I'm in focus mode, I wish I can control the mouse pointer with my eyes. I don't want to break my focusing by touching the mouse. 

One day, I've heard what my colleague said about automation. "The first point of building automation process is whether someone can recognize the annoyance." I 100% agree with that point. And, I want to ask about "What are your annoyances typing or editing your code?" Have you tried to find or realize something? Ok. That's the starting point. 

# Pycharm Productivity guide
When we face some difficulty or not knowing how to do, what are we going to do? Me? I'm going to find Google. I usually search some of the features by searching. But, it's not applicable always since it does not easy to explain my situation. What if the IDE analyses features that I use and shows what you never use some features? Can we get benefit from the statistics? 

![pycharm productivity guide](/assets/images/2021/01/30/py_prod_guide.png)

This feature does that right for you; [Pycharm productivity guide](https://www.jetbrains.com/help/pycharm/using-productivity-guide.html). I've never thought it could be possible. I heard that we could analyze where the user mostly stayed in the program or website. One warning here. I guess this feature is not included in the Community version. I can find it in the Professional version of it. 

# Remote debugging 
One of the most powerful feature that I use every day is debugging remotely. Jupyter notebook is popular because of the way it prints the result of execution immediately. It is possible using Pycharm. You can attach the debugger while running on your remote server machine. You can run your Python script in your server even you can debug line by line. You only need to set up the remote configuration. I'm not going to explain how to set it up since [the official document](https://www.jetbrains.com/help/pycharm/remote-debugging-with-product.html#remote-interpreter) already shows the exact steps to follow. 

One major drawback of the Jupyter notebook is reproducibility. If we work on Pycharm, we can create reusable code using SOLID pattern; Creating some classes, and modularize. However, in the Jupyter notebook, we may prefer to copy and paste the code, which isn't maintainable or reproducible. 

Plus, I've tried the remote debugging feature in the Professional version of Pycharm. So that, it may not work in the Community edition. If you know, please leave me any comments. 

# Outro 
In this short post, I'm talking about two daily features of Pycharm that can boost your productivity. I heavily rely on the remote debugging feature. It breaks the gap of environment between local and server. I can't imagine how come I have any trouble without that. If you haven't tried it; a Productivity guide and Remote debugging, why don't you try those features? 