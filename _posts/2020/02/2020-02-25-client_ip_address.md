---
title: "How to get a client IP address? Nginx - Docker - Gunicorn - Django"
excerpt: "Interms of service, how to figure out client IP address"
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-25T08:06:00-05:00
---

## Story 
A week ago, I built a simple API server. I need to enable HTTPS access and I don't know how to do it. So, I got help for setting up the Nginx server from my colleague. That's fine but an issue came out. I want to get a client IP address because I need to prepare an attack situation. To cope with the attack situation, I created a log file but all client IP addresses were the same. It seemed like a gateway IP address from a Docker container. To debug the issue, we used tcpdump and we found out what was going wrong. In this post, I will introduce how to figure out a client IP address.

## Environment 
* Ubuntu 16.04 
* Docker 18.09.7, build 2d0083d
* Gunicorn 20.0.4
* Nginx 1.10.3
* Django >= 2.2.4

As a precaution, we need to take consider when bunch of requests are comming. We decided to deploy using a docker and gunicorn to scale easily. Our big picture is Nginx - Docker - Gunicorn - Django flow.
Since there might be a little chance , we deploy it by using docker. Our big picture is Nginx - Docker - Gunicorn - Django flow.

## How to? 

At first, we have to change the Nginx configuration.

```
# ... keep above settings
# Nginx

http{
    location{
        proxy_redirect off;
        proxy_set_header REMOTE_ADDR $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# ... keep below settings 
```

We need to install a middleware and it's [here](https://pypi.org/project/django-xff/).

```python
# settings.py 
MIDDLEWARE = [
    'xff.middleware.XForwardedForMiddleware',
]
```

Finally, I find the client IP address.

```python
def get_client_ip(request):
    x_forwarded_for = request.META.get('HTTP_REMOTE_ADDR')
    if x_forwarded_for:
        ip = x_forwarded_for.split(',')[0]
    else:
        ip = request.META.get('REMOTE_ADDR')
    return ip
```

That's all. I hope you can solve you problem. Thank you.