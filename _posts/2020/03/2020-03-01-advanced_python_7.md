---
title: "Logging in Python"
excerpt: ""
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-03-01T08:06:00-05:00
---

## Python Logging

Why do we need the logging feature? Because we might have a slightly different environment between debug and release, in the release environment, it may raise a strange error. We can use a debugger in the modern IDE environment such as Pycharm and Visual Studio Code. But, when we work on the server-side, I know some C language codes can be debugged by GDB. It's not always as easy just like that case. Instead of debugging, we can keep log files to audit what codes of the program have been executed. 

* Captures and records events while app is running
* Useful debugging feature 
    * Not always practical to debug in real time
* Events can be categorized for easier analysis
* Provides transaction record of a program's execution
* Highly customizable output


## Basic Logging

```python
import logging 


def demo():
    logging.basicConfig(level=logging.DEBUG)

    logging.debug("This is a debug message")
    # DEBUG:root:This is a debug message
    logging.info("This is a info message")
    # INFO:root:This is a info message
    logging.warning("This is a warning message")
    # WARNING:root:This is a warning message
    logging.error("This is an error message")
    # ERROR:root:This is an error message
    logging.critical("This is a critical message")
    # CRITICAL:root:This is a critical message

demo()
```

* logging.debug(): Diagnostic information useful for debugging
* logging.info(): General information about program execution results
* logging.warning(): Something unexpected, or an approaching problem
* logging.error(): Unable to perform a specific operation due to program
* logging.critical(): Program may not be able to continue, serious error 

```python
logging.basicConfig(level=logging.DEBUG)
```
In the logging module, we can find 5 types of logging levels. Each has own purpose for logging. The basicConfig function won't affect the code after one of those logging function is called. So, it should be at the top of the code to set the default logging level. 


## Customized Logging
```python
extData = {
    'user': 'devjunhong@example.com'
}


def anotherFunction():
    logging.debug("This is a debug-level message", 
    extra=extData)
    # User:devjunhong@example.com 03/01/2020 08:37:30 AM: 
    # DEBUG: anotherFunction Line:516 
    # This is a debug-level message


def demo():
    fmtstr = "User:%(user)s %(asctime)s: %(levelname)s: \
%(funcName)s Line:%(lineno)d %(message)s" # [1]
    datestr = "%m/%d/%Y %I:%M:%S %p" # [2]
    logging.basicConfig(filename="output.log",
    level=logging.DEBUG,
    format=fmtstr,
    datefmt=datestr)
    
    logging.info("This is an info-level log message", 
    extra=extData)
    # User:devjunhong@example.com 03/01/2020 08:37:30 AM: 
    # INFO: demo Line:532 
    # This is an info-level log message
    logging.warning("This is a warning-level message", 
    extra=extData)
    # User:devjunhong@example.com 03/01/2020 08:37:30 AM: 
    # WARNING: demo Line:533 
    # This is a warning-level message
    anotherFunction()


demo()
```

We can customize our log result by sending format and datefmt arguments. As we can see [1] and [2], we passed custom format and we find results on the 'output.log' file. In this example, we can observe results in the file not on the console. In the [1] format string, we can add manual token by using a dictionary(extData).

```python
basicConfig(
    format=formatstr,
    datefmt=date_format_str
)
```

* %(asctime)s: Human readable date format when the log record was created
* %(filename)s: File name where the log message originated
* %(funcName)s: Function name where the log message originated
* %(levelname)s: String representation of the message level (DEBUG, INFO, etc.)
* %(levelno)d: Numeric representation of the message level 
* %(lineno)d: Source line number where the logging call was issued (if available)
* %(message)s: The logged message string itself
* %(module)s: Module name portion of the filename where the message was logged. 

These formatted tokens are frequently used to format a log.