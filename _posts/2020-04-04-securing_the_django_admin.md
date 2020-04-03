---
title: "Securing the Django admin"
excerpt: "How to make sure security for admin"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-04-04T08:06:00-05:00
---

This post is followed by this [article](https://devjunhong.github.io/django/security_in_django/). In this post, we want to add security features to our Django admin site.  


## Make secure your Admin

* Change Admin URL 
    * Change it to something difficult to guess. Keeping /admin/ makes your site easy to profile and is an easy starting point for attackers. 
    * Action
        ```python
        # urls.py 
        url(r'^admin/', admin.site.urls),
        ```


* Secure or Remove Admin Docs
    * Your site docs tell a lot about your site and how it's constructed 
    * Change or remove the URL to help protect your site
    * Action
        ```python
        # urls.py
        django.contrib.admindocs.urls
        ```


* Only Allow Access over HTTPS 
    * Without HTTPS/SSL it would be trivial to sniff your admin's username and password
    * Action
        ```python
        # settings.py 
        SECURE_SSL_DIRECT = True
        SESSION_COOKIE_SECURE = True 
        CSRF_COOKIE_SECURE = True 
        ```


* Limit Access Based on IP 
    * Most if not all web servers provide a way to limit access to a URL based on IP 
    * This logic could also be put into middleware too 
    * Action 
        * Procedure changes based on your server 


* Use django-admin-honeypot
    * django-admin-honeypot is a fake Django admin login screen to log and notify admins of attempted unauthorized access
    * Action 
        * [django-admin-honeypot repository](https://github.com/dmpayton/django-admin-honeypot)


* Use strong passwords 
    * django-passwords is a reusable app that provides a form field and validators that check the strength of a password 
    * Action 
        * [django-passwords](https://github.com/dstufft/django-passwords)