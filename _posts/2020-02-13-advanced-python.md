---
title: "Why Python and PEP to keep the rule"
excerpt: "I want to share what I learn from a python course."
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-13T08:06:00-05:00
---

## Why Python?
![Python skyrocket](/assets/images/python_popularity.png)
You can check out the blue line skyrocket. This is Python. I write code in C#, VB.NET, Javascript, Java, C++, and Python. When I write code in Python, I feel the grammar of Python doesn't block my think flow and also easy to learn. Sometimes it gives me strange error because of strict indentation rule. But I have witnessed several times length comparison between C++ and Python. If both codes do the same thing then usually, Python is much shorter than C++. This makes me feel Python is easy.

```c++
//C++
#include <stdio>

using namespace std;

int main() {
    string name;
    cin >> name;
    cout << "Good evening, " << name << endl;
    return 0;
}
```

```python
# Python
name = input()
print("Good evening, " + name)
```
The above codes in C++ and Python do the same thing. Getting a user input and printout the name with a good evening message. 

We can check the big named company use Python; Google, Dropbox, Netflix, and Nasa.
![Python in real](/assets/images/big_named_python.png)


## Before coding
Before deep dive into programming directly, we'd better learn a coding style. Every day in my job, I spend more time to read codes than writing codes. A strong coding style makes it easy. Some languages officially have a coding style. Python has a PEP(Python Enhancement Proposal) coding style rule. 


## PEP8
The full name of PEP is Python Enhancement Proposal and here is a link for [the original document](https://www.python.org/dev/peps/pep-0008/). 

If you use Pycharm, the editor is so powerful. It checks all the PEP8 rules and reports with waved underline. Here is a brief list of PEP8.

* Indent code using spaces instead of tabs
* Use four spaces for each indentation level 
* Limit lines to 79 characters (72 for docstrings/comments)
* Separate functions and classes by two blank lines
* Within classes, separate methods by one blank line
* No spaces around function calls, indexes, keyword arguments

For limiting the lines to 79 characters, I've understood this rule is adapted because of screen size. But, this can also apply when I have to open diff tools. When you write on one screen and split it vertically, this rule has a big benefit because you don't need to scroll horizontally. 