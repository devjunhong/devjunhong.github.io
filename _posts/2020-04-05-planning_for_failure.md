---
title: "Planning for failure"
excerpt: "How to make sure security for admin"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-04-04T08:06:00-05:00
---


This post is followed by [this article](https://devjunhong.github.io/django/securing_the_django_admin/). 


## Pre Failure 

* Start backing up everything 
* Most sites provide built-in backup tools (Linode, AWS, Digital Ocean) 
* If you work for a business, buy an enterprise solution
* Backups can be expensive, but losing sensitive data and having downtime is more expensive 


## Keep Calm Failures happen 

* Step 1: Block Access 
    * Shut down your site or start a Read-Only mode (django-db-tools)
    * It is all about minimizing damage
    * If someone has gained access to your site you need to make sure they do as little damage as possible
    * This can be done through taking the site down or enabling a read-only mode so data cannot be changed 

* Step 2: Enable Maintenance Page 
    * Static HTML Pages or Read-Only Pages
    * You can't leave your customers or co-workers in the dark 
    * Take a moment to put in place a prepared maintenance page

* Step 3: Backup Everything
    * This protects current "new" data as well as protecting your security audit trail 

* Step 4: Get some help 
    * Email: security@djangoproject.com
    * Django IRC: #django freenode.net
    * other forums: https://security.stackexchange.com
    * Even if it's not a Django problem Django's community will help!

* Step 5: Start Debugging 
    * Breath, Keep Calm, Stay Positive!
    * Start figuring out where the problem started and how

