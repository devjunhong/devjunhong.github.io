---
title: "Enumeration, Class String and Attribute Functions, Class Numerical and Comparison Operators"
excerpt: "A list of sample Python code using those features"
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-27T08:06:00-05:00
---

## Advanced Classes
* Create enumerations
* Customize string and byte representations of objects
* Define computed and default attributes
* Control how objects are logically compared to each other
* Give objects numeric-like behavior (addition, subtraction, etc.)

In this post, we gonna look through the above features in Python one by one with simple example code. 

## Enumeration 
```python
from enum import Enum, unique, auto


@unique
class Fruit(Enum):
    APPLE = 1
    BANANA = 2
    ORANGE = 3
    TOMATO = 4
    # APPLE = 1 # [1] Error
    # RED_DEILICIOUS = 1 # [2] Error
    PEAR = auto()


def demo_enum():
    print(Fruit.APPLE)
    # Fruit.APPLE
    print(type(Fruit.APPLE))
    # <enum 'Fruit'>
    print(repr(Fruit.APPLE))
    # <Fruit.APPLE: 1>

    print(Fruit.APPLE.name, Fruit.APPLE.value)
    # APPLE 1
    print(Fruit.PEAR.value)
    # [3] 5

    myFruits = {}
    myFruits[Fruit.BANANA] = "Mr. Tally-man"
    print(myFruits[Fruit.BANANA])
    # Mr. Tally-man


demo_enum()
```
The Enum class makes your code more readable. As we can see the [1], Enum can't have the same name as the key. If we care about values to be unique, then we'd better have the unique decorator. So that it can raise an error just like [2]. Enum supports auto-increment as we can observe in the [3]. I used Enum structure in C language a lot to control a logic flow to avoid anonymous literal. 

## Class String Functions

```python 
class Person:
    def __init__(self):
        self.fname = "Joe"
        self.lname = "Marini" 
        self.age = 25

    def __repr__(self):
        return "<fname:{0}, lanme: {1}, age: {2}>"\
        .format(self.fname, self.lname, self.age)

    def __str__(self):
        return "Person ({0} {1} is {2})"\
        .format(self.fname, self.lname, self.age)

    def __bytes__(self):
        val = "Person:{0}:{1}:{2}".\
        format(self.fname, self.lname, self.age)
        return bytes(val.encode('utf-8'))


def demo():
    cls1 = Person()

    print(repr(cls1))
    # <fname:Joe, lanme: Marini, age: 25>
    print(str(cls1))
    # Person (Joe Marini is 25)
    print("Formatted: {0}".format(cls1))
    # Formatted: Person (Joe Marini is 25)
    print(bytes(cls1))
    # b'Person:Joe:Marini:25'


demo()
```

* object.\__str__(self): str(object), print(object), "{0}".format(object)
* object.\__repr__(self): repr(object) 
* object.\__format__(self, format_spec): format(object, format_spec)
* object.\__bytes__(self): bytes(object)

An object can override these string functions. The repr function is usually used for debugging. 

## Class Attribute Functions 

```python
class myColor:
    def __init__(self):
        self.red = 50
        self.green = 75
        self.blue = 100

    def __getattr__(self, attr):
        if attr == 'rgbcolor':
            return (self.red, self.green, self.blue)
        elif attr == 'hexcolor':
            return '#{0:02x}{1:02x}{2:02x}'.format(
                self.red, self.green, self.blue
            )
        else:
            raise AttributeError

    def __setattr__(self, attr, val):
        if attr == 'rgbcolor':
            self.red = val[0]
            self.green = val[1]
            self.blue = val[2]
        else:
            # important to call this
            super().__setattr__(attr, val)

    def __dir__(self):
        return ('red', 'green', 'blue', \
            'rgbcolor', 'hexcolor')

def demo_attr():
    cls1 = myColor()

    print(cls1.rgbcolor)
    # (50, 75, 100)
    print(cls1.hexcolor)
    # #324b64

    cls1.rgbcolor = (125, 200, 86)
    print(cls1.rgbcolor)
    # (125, 200, 86)
    print(cls1.hexcolor)
    # #7dc856

    print(cls1.red)
    # 125

    print(dir(cls1))
    # ['blue', 'green', 'hexcolor', 'red', 'rgbcolor']
```

* object.\__getattribute__(self, attr): object.attr
* object.\__getattr__(self, attr): object.attr
* object.\__setattr__(self, attr, val): object.attr = val
* object.\__delattr__(self): del object.attr
* object.\__dir__(self): dir(object)

If we use other attributes instead of defining as a member of an object, we can use the above functions to create additional attributes. The 'getattribute' and 'getattr' functions look the same but slightly different. 'getattribute' function will be unconditionally called every time, however 'getattr' function will be called when there're no requested attributes in the class. 

## Class Numerical Operators

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        return "<Point x:{0}, y:{1}>"\
            .format(self.x, self.y)

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Point(self.x - other.x, self.y - other.y)

    def __iadd__(self, other):
        self.x += other.x
        self.y += other.y
        return self


def demo():
    p1 = Point(10, 20)
    p2 = Point(30, 30)
    print(p1, p2)
    # <Point x:10, y:20> <Point x:30, y:30>

    p3 = p1 + p2
    print(p3)
    # <Point x:40, y:50>

    p4 = p2 - p1
    print(p4)
    # <Point x:20, y:10>

    p1 += p2
    print(p1)
    # <Point x:40, y:50>


demo()
```
* object.\__add__(self, other): self + other
* object.\__sub__(self, other): self - other
* object.\__mul__(self, other): self * other
* object.\__div__(self, other): self / other
* object.\__floordiv__(self, other): self // other
* object.\__pow__(self, other): self ** other 
* object.\__and__(self, other): self & other
* object.\__or__(self, other): self \| other

* object.\__iadd__(self, other): self += other
* object.\__isub__(self, other): self -= other
* object.\__imul__(self, other): self *= other
* object.\__itruediv__(self, other): self /= other
* object.\__ifloordiv__(self, other): self //= other
* object.\__ipow__(self, other): self **= other 
* object.\__iand__(self, other): self &= other
* object.\__ior__(self, other): self \|= other

A Class can override the above mathematical operations. We can override in place operation too.


## Class Comparison Operators 

```python
class Employee:
    def __init__(self, fname, lname, level, yrsService):
        self.fname = fname
        self.lname = lname 
        self.level = level 
        self.seniority = yrsService

    def __ge__(self, other):
        if self.level == other.level: 
            return self.seniority >= other.seniority
        return self.level >= other.level 

    def __gt__(self, other): 
        if self.level == other.level: 
            return self.seniority > other.seniority
        return self.level > other.level

    def __lt__(self, other):
        if self.level == other.level: 
            return self.seniority < other.seniority
        return self.level < other.level

    def __le__(self, other):
        if self.level == other.level: 
            return self.seniority <= other.seniority
        return self.level <= other.level


def demo_class_comparisson():
    dept = []
    dept.append(Employee("Tim", "Sims", 5, 9))
    dept.append(Employee("John", "Doe", 4, 12))
    dept.append(Employee("Jane", "Smith", 6, 6))
    dept.append(Employee("Rebecca", "Robinson", 5, 13))
    dept.append(Employee("Tyler", "Durden", 5, 12))

    print(dept[0] > dept[2])
    # False
    print(dept[4] < dept[3])
    # True

    emps = sorted(dept)
    for emp in emps:
        print(emp.lname)

        # Doe
        # Sims  
        # Durden
        # Robinson
        # Smith
```

* object.\__gt__(self, other): self > other
* object.\__ge__(self, other): self >= other
* object.\__lt__(self, other): self < other
* object.\__le__(self, other): self <= other
* object.\__eq__(self, other): self == other 
* object.\__ne__(self, other): self != other 

We can sort our custom class by overriding the above functions. The naming rule of those functions abbreviate a full operation name. 'gt' means 'greater than', 'ge' means 'greater or equal to'. 