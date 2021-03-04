---
title: "Check ssh availability using cron in Mac"
excerpt: "Deal server hanging issues"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/03/04/server.jpg
  # image: /assets/images/2021/02/06/soft_skills_v2.jpeg
  caption: "Photo by [Massimo Botturi](https://unsplash.com/@wildmax?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/server?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)"
  
  # og_image: /assets/images/2021/02/06/soft_skills_v2.jpeg
layout: single
# classes: wide
word-wrap: break-word;
categories:
    - Server
tags:
    - Server
last_modified_at: 2021-03-04T08:06:00-05:00
---

# Intro 
Dealing with hanging problems in a server closes to magic. If it is a magic, can we detour or fast respond when it happens? To be ready, it is required to have an automated script. In this post, I'm going to write about how to detect the availability of ssh access to servers using a shell script. 

# Big picture 
1. [Implement a shell script](#first)
2. [Register using cron](#second)
3. [Allow cron to access a full disk](#third)
4. [Check up the mail in Mac](#fourth)

## <a name="first">1 - Implement a shell script</a>
```sh
# enter_ip_addresses, ex) 192.0.0.1 192.0.0.2 ...
for ip in enter_ip_addresses
do
    nc -vz $ip $1 -w 5
    if [ $? == 0 ]
    then
        echo "${ip} ssh is available"
    else
# mail_address_here, ex) abc@abc.com
        echo "${ip} ssh is not available, please contact somebody" | mail -s $ip mail_address_here
    fi
    echo $?
done
```
Okay, break down the script a little bit. The for-loop iterates a single IP address. The nc command checks up ssh availability to your server and it times out after 5 seconds. If there's no problem it shows ssh is available, and if not it will send an email using a body message (x.x.x.x ssh is not available, please contact somebody). 


## <a name="second">2 - Register using cron</a>
```sh
crontab -e 
```
We have to register the execution command using cron. This site helps you to write the cron command. [https://crontab.guru/](https://crontab.guru/) If you want to check the cron works, you'd better to use short periodic work such as setting it as every minute. (* * * * *)

## <a name="third">3 - Allow cron to access a full disk</a>
Here is the thread about allowing access to full disk by cron. [https://serverfault.com/a/1012212](https://serverfault.com/a/1012212) If your environment is mac, you need to allow cron to access the disk. 

## <a name="fourth">4 - Check up the mail in Mac</a>
```sh
mail 
```
By entering mail in your command-line interface, you can check up results of cron works. If it says "Operation is not permitted", make sure you [allow access to the disk by cron](#third). 

# Outro 

I hope this makes your work automated and I want that you don't suffer server hang issues. Thanks.
