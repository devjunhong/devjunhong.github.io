---
title: "Method Resolution Order and mixins"
excerpt: "understand how mixins work in Django"
toc: true
toc_sticky: true 

categories:
    - Django
tags:
    - Django
last_modified_at: 2020-03-10T08:06:00-05:00
---

## Method Resolution Order (MRO) 

```python
class Parent1:
    def speak(self):
        print("I am Parent1")

    def talk(self):
        print("Parent1 talking")


class Parent2:
    def speak(self):
        print("I am Parent2")


class Child(Parent2, Parent1):
    pass 


child = Child()
child.speak()
# I am Parent2
child.talk()
# Parent1 talking
```

We can see the speak method is declared in both Parent1 and Parent2 classes. Which one will be executed? In this case, we have to understand the method resolution order. In Python, a method that can be found in the left-most parent class will be executed. So, in this case, Parent2 has the 'speak' method and it will print out. 


It's time to find the 'talk' method. Firstly, the Python will take a look at the Child class and there's no 'talk' method. So, next search the method in Parent2. Finally, it will see where the 'talk' method is. The Parent1's will be printed out. It's the way how to find a method under the inheritance.

```python
class Parent1:
    def speak(self):
        print("I am Parent1")

    def talk(self):
        print("Parent1 talking")


class Parent2:
    def speak(self):
        print("I am Parent2")
        return super(Parent2, self).speak() # [1]


class Child(Parent2, Parent1):
    pass 


child = Child()
child.speak()
# I am Parent2
# I am Parent1
child.talk()
# Parent1 talking
```

The only difference is that [1] is added and it makes the Python keep search the 'speak' method over the method resolution order. So, the result will be different. The Parent2's speak method will be printed out first and then it will show the Parent1's speak method too. This knowledge will help to understand what mixins do in Django. 


## mixins 

* Modular functionality 
* Keeps code DRY (Don't Repeat Yourself)

To follow the related code about mixins, we need to understand what method resolution order is. In the above, I write about it. In Django, by using mixins we will achieve modular functionality and keep our code DRY. 