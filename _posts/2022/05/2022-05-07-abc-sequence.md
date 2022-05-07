---
title: "collections.abc.Sequence"
excerpt: "Python built-in sequence types are `list`, `str`, `tuple`, and `bytes`"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2022/05/collections_abc_sequence.png
  # image: /assets/images/2022/04/range_python.png
  # caption: "Photo by [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/python?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  
  og_image: /assets/images/2022/05/collections_abc_sequence.png
layout: single
# classes: wide
word-wrap: break-word;
categories:
    - Python
tags:
    - Python
last_modified_at: 2022-05-07T06:43:00-05:00
---

In [the last posting](https://devjunhong.github.io/python/what-is-range-in-python/#is-this-a-generator), I've written about the range. In Python, the range object is an implementation of `collections.abc.Sequence`. Let's take a look at what it is. 

# collections.abc.Sequence 

## abc? 
Here "abc" is "Abstract Base Class". 

## Abstract class
Quoting from the Wikipedia, 
> In programming languages, an abstract type is a type in a nominative type system that cannot be instantiated directly. 

Two new terms are here. "nominative type system" and "instantiate". 

Again quoting from the Wiki page,
> Nominal typing means that two variables are type-compatible if and only if their declarations name the same type. 

To understand this with an example, [this article](https://medium.com/@thejameskyle/type-systems-structural-vs-nominal-typing-explained-56511dd969f4) is great to understand in a programming context. 

In a nutshell, "Nominal typing" raises an error if we place a different type of variable to the expected type even though the difference is just the name of the type.

On the other hand, "Structural typing" says it's okay. Once we modify the content, it will raise an error. 

"Instantiation" in Python is creating an instance from a class definition. 

```Python 
class foo:
  ...

f = foo()
```

This is a side note from the Python official document. 

> Some of the mixin methods, such as __iter__(), __reversed__() and index(), make repeated calls to the underlying __getitem__() method. Consequently, if __getitem__() is implemented with constant access speed, the mixin methods will have linear performance; however, if the underlying method is linear (as it would be with a linked list), the mixins will have quadratic performance and will likely need to be overridden.

## mixin? 
For me, the multiple inheritance concept is more clear than mixin. For example, this is the inheritance in Python. 

```python
class Animal(): 
  def sound(self): 
    return ""


class Duck(Animal): 
  def sound(self): 
    return "quack"


class Dog(Animal): 
  pass 

duck = Duck()
duck.sound()  # 'quack'

dog = Dog()
dog.sound()  # ''

```
The child class inherits its parent class's function and member variables. 

Multiple inheritances are having multiple classes as parents. However, in practice, it's super brittle to use multiple inheritances. In the community, it's not the recommended way to design classes. 

Mixin wants to address the inefficiency in single inheritance and the difficulty of multiple inheritances. 

The mixins can offer rich behaviors to the target class. We expect those mixins will not be instantiated by themselves. 

The concept of mixins is very similar to the multiple inheritances.

We want to gain advantages of the multiple inheritances and avoid the complexity. 


# Glossary "Sequence"
* Supports efficient element access using integer indices via the `__getitem__()` special method and defines a `__len__()` method that returns the length of the sequence. 
* Built-in sequence types are `list`, `str`, `tuple`, and `bytes`
* `dict` also supports `__getitem__()` and `__len__()` but is considered a mapping because the lookups using arbitrary [immutable](https://devjunhong.github.io/python/what-is-range-in-python/#what-is-immutable) keys rather than integers

# Reference 
* [Python doc Sequence](https://docs.python.org/3/library/collections.abc.html#collections.abc.Sequence)
* [Python Glossary Doc](https://docs.python.org/3/glossary.html#term-sequence)
* [Abstract type, from wiki](https://en.wikipedia.org/wiki/Abstract_type)
* [Nominal type system, wiki](https://en.wikipedia.org/wiki/Nominal_type_system)
* [TypeSystems](https://medium.com/@thejameskyle/type-systems-structural-vs-nominal-typing-explained-56511dd969f4)
* [Python Mixins](https://www.residentmar.io/2019/07/07/python-mixins.html)
* [Mixin and multiple inheritance](https://stackoverflow.com/questions/533631/what-is-a-mixin-and-why-is-it-useful)