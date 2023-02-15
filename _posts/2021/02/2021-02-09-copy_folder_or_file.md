---
title: "Copy folder or file using the result of ls command"
excerpt: "bash command can save your time"
toc: true
toc_sticky: true
published: true
header:
  # teaser: /assets/images/2021/02/06/soft_skills_v2.jpeg
  # image: /assets/images/2021/02/06/soft_skills_v2.jpeg
  # caption: "Photo by me"
  # og_image: /assets/images/2021/02/06/soft_skills_v2.jpeg
layout: single
classes: wide

categories:
    - Bash
tags:
    - shell script
last_modified_at: 2021-02-09T08:06:00-05:00
---

# Situation
If you want to copy the list of files or folders using outputs of the ls command, you may find this post is useful. One simple bash command line can save your time. 

## Example 
You might need to copy all the mp4 files in a directory to another directory. Here is an example folder structure. 
```text 
/a/video1.mp4
/a/video2.mp4
/a/video3.mp4
```
How can we copy those mp4 files to directory b? 
```sh 
cp `ls /a | grep "*.mp4" | perl -ne 'print "/a/$_"'` /b
```

That's it. All done! Here is the general form of the command. 

```sh
cp -R `ls /path/to/source | grep -E "target" | perl -ne 'print "/path/to/source/$_"'` ./
```

# Backtick 
Inside of the command between backtick will be evaluated by the shell before the main command. [Article](https://unix.stackexchange.com/a/27432)

# grep with E option 
The E option escape certain special characters for example, '{' or '('. [Article](https://unix.stackexchange.com/a/50514)

# perl with -ne option 
The "perl" command uses the Perl programming language. 

-n: causes perl to assume the following loop around your script, 


-e: maybe used to enter one line of script. 

[Here](https://www.perl.com/pub/2004/08/09/commandline.html/) is the article about Perl options. 

Hene, the command line prints the output of the filename concatenated with the absolute path. I use the perl command to concatenate the original absolute path. [Article](https://stackoverflow.com/a/26783959)


