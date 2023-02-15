---
title: "CLI environment"
excerpt: "My daily tools that I use when I have a server work"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/25/iterm.png
#   image: /assets/images/2021/01/24/openface_og_updated.png
#   caption: "Photo by me"
#   og_image: /assets/images/2021/01/24/openface_og_updated.png
layout: single
# classes: wide

categories:
    - CLI
tags:
    - tmux 
    - iTerm 
    - Fish
    - screen
last_modified_at: 2021-01-25T08:06:00-05:00
---

# Intro 
As a deep learning engineer, my daily work involves working on a Linux server; setting up the firewall, creating an account for a newcomer, cleaning up the disk space, and communicating with a data center service provider. Frankly, it does not look like a deep learning engineer's work. Since I'm working in a small startup, I need to handle various works simultaneously. Anyway, I always have in mind how others work effectively with CLI(Command Line Interface) environment. Please leave me a comment, if you know a better way or smart tools. So, at least, I can check it up. 

In this post, I'm going to share my environments when I am working on a Linux console. I'm hungry to boost my productivity, so please share yours too. 

# Terminal
## <a name="iterm">iTerm</a> (macOS) 
[iTerm](https://iterm2.com/index.html) is a terminal program for macOS. The first program that I want to install on my new Macbook. One picture is better than 1000 words. 

![iterm](/assets/images/2021/01/25/iterm.png) 

I named each tab here. Using the iTerm, I can create tabs, name on it, and even colors on it. For me, the best feature is saving commands for accessing the server. It saves accessing commands like "ssh blah blah" as a profile, and I can categorize it. 

![iterm](/assets/images/2021/01/25/iterm_new_tabs.png)

I have a bunch of profiles on a machine in the office. Here, to make an example, I take a picture of mine; a private.

I know I have room to improve my usage of iTerm. I want to hear your idea or use case, so please leave me any comment. 

## <a name="konsole">Konsole</a> (Ubuntu)
When I work for a company, I use Ubuntu 20.04.1 LTS. I want to find an iTerm like experience in Ubuntu. The result is this; [Konsole](https://konsole.kde.org/). As in the iTerm, my best feature is the profile to save the access information of servers. 

It is possible to have a transparent background on the screen. I feel it's useful when a search results in my background and cover the result by the transparent screen. I can type the command without change the screen. If I have a dual monitor, then I need to move one screen to another screen. When you have a transparent background, you are not going to use mouse, but you just cover it.

# Window manager
## <a name="tmux">tmux</a>
Here, after access to the server using the [iTerm](#iterm) or [Konsole](#konsole). It's time to work on the real CLI environment. I prefer [tmux](https://github.com/tmux/tmux/wiki) because of its powerful feature dividing screens horizontally and vertically by keyboard shortcut. 

![image](/assets/images/2021/01/25/tmux.png) 

With a little effort to learn the cheatsheet about tmux, I think this boosts your productivity when you frequently open a new session by using the ssh command. Since we can use our full space of the screen, we can stay on a single monitor environment too. For me, this is the best feature of tmux, and here is the [cheatsheet](https://tmuxcheatsheet.com/). 

## screen 
[Screen](https://www.gnu.org/software/screen/) is like the [tmux](#tmux). It manages the window. Let's say you are going to install a huge package and you want to get out on the screen since you don't want to waste time by waiting for the installation. Let's use screen in this case. Creating one screen and entering on it, you can use a shell whatever you prefer. Hitting the installation command and push "Ctrl-a + d". It lets you out of the screen. The keyboard operations means detach the screen. This is one simple example to use the screen. 

![list of screens](/assets/images/2021/01/25/screen.png)

# Shell
## fish shell
A friendly interactive shell is the [Fish shell](https://fishshell.com/). The best feature of this is remembering. If you keep the same command repeatedly, you definitely feel you don't want to type the same command more. That's the case. The fish shell makes you free to type the same command again and again. 

![fish shell auto-complete](/assets/images/2021/01/25/fish_shell.png) 

See the grey command. It's ready to type the command by hitting the shortcut. Here's the [cheatsheet](https://devhints.io/fish-shell) for the fish shell. 

# Outro 
While writing this post, I've found several new features on each program. I need to revisit those useful features. Recently, when I'm free, I want to learn about my tools because I feel like I'm using the very basic. Times fly, and now we are in the middle of the Pandemic. Still, a monkey can't fly, but we, as a programmer, develop our tool a lot.  In the long-term, those trials to learn our tool saves our time; the priceless one. 

