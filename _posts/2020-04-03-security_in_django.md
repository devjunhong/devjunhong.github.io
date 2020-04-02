---
title: "Security in Django"
excerpt: "Create secure application"
toc: true
toc_sticky: true

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-04-03T08:06:00-05:00
---


Building a secure software become more important in thesedays. Django provides some of default security feature. Let's take a look at it. 


## Built in security for 
* Cross Site Scripting (XSS)
* Cross Site Request Forgery (CSRF)
* SQL injection 
* Support for HTTPS and TLS 
* Secure Password Storage


| Attack Name                       | Descrpition                                                                                                                                  | Django helps by                                                                                                                                                                                                         |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cross Site Scripting (XSS)        | XSS enables attackers to inject client-side scripts into web pages viewed by other users                                                     | Automatically escaping data dynamically inserted into templates                                                                                                                                                         |
| Cross Site Request Forgery (CSRF) | An exploit of a website where unauthorized commands are transmitted from a user that the web application trusts                              | Providing a built in csrf_token template tag and csrftoken cookie                                                                                                                                                 |
| SQL Injection                     | A code injection technique, used to attack data-driven applications, in which SQL statements are inserted into an entry field for execution  | Providing a power ORM. As long as .raw() and .extra() are avoided SQL Injection is nearly impossible                                                                                                                    |
| Support for HTTPS and TLS         | An adaptation of the Hypertext Transfer Protocol (HTTP) for secure communication over a computer network, and is widely used on the internet | * Providing SECURE_SSL_REDIRECT to redirect requests over HTTP to HTTPS <br><br>* Providing SESSION_COOKIE_SECURE and CSRF_COOKIE_SECURE to secure cookies and POST requests                                                  |
| Secure Password Storage           |                                                                                                                                              | * Never storing plain text passwords <br><br>* Providing a flexible password storage system and uses PBKDF2 by default<br><br>* Using the PBKDF2 algorithm with a SHA256 hash, a password stretching mechanism recommended by NIST |
|                                   |                                                                                                                                              |                                                                                                                                                                                                                         |