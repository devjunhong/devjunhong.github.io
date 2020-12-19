---
title: "About Rust memory safety"
excerpt: "I took a Udemy course"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2020-12/rustacean.png
  og_image: /assets/images/2020-12/rustacean.png

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2020-12-17T08:06:00-05:00
---

Rust has these advantages; Let's figure them out one by one. [[1]](#first)

* Memory safe
* Have no Null type
* No Exceptions
* Modern package manager
* No Data Races

# Memory Safe 
In the computer system, there are two types of memory regions; [Stack](#stack) and [Heap](#heap). When a program executes a function, a memory of the function will be pushed in the Stack region. It will be on top of the Stack, and it pops out when the execution of the function is over. The [operating system](#os) limits the Stack region. If we pile something up on the Stack area endlessly, we might encounter the  [Stack overflow error](#stack-overflow).  
The second is the Heap region. In C or C++, when we need a dynamic memory space, (We have no idea before run-time how much we need a size of memory.) we call the [malloc](#malloc) function to do that. This is the case using the Heap area. The crucial point is we need to manage the Heap region very carefully. If we forget to deallocate the memory, then we will face a memory leak. Usually, the fault brings vulnerable attack space. 

Let me show you what example can raise unsafe use of memory with pseudo-code. 
```
function main()
  call example 

function example()
  a = 3
  b = allocate 5

call main
```

In the code, it calls the main function, and it calls the example function again. In the example function, the variable 'a' will be stored in the Stack area and the variable 'b' will be stored in the Heap region. (5 does not look like to be determined on the run-time. Here, for sake of simplicity, I use 5.) When we call the allocate function, it returns a pointer according to [malloc](#malloc). The pointer means a specific address of memory. The value 5 is stored in the Heap area and we can access it with the memory(pointer). After the example function is over, we have no idea about how to access the value 5, since we didn't have the memory address. This is where the [memory leak](#memory-leak) happens. It can cause a security issue. 

To cope with the problem, we need to deallocate all the unused Heap memory addresses. Unfortunately, humans forget some important things easily. In C++, [Smart Pointer](#smart-pointer) is introduced to overcome this issue. It's a wrapper for the memory address and it deallocates the memory when it's out of use. 

## TLDR
We consider memory management while we are using C/C++. If we are able to use [Smart Pointer](#smart-pointer), I think it's the best choice. In Rust, the Rust compiler takes all over. What does it mean? It does not happen in Rust. How? Rust destroys all variables when the variable is out of scope. I think Rust prevent memory leak, but that's not true. We can still create the memory leak issue by these tricks. [[9]](#ninth)



# Terms
## <a name="stack">Stack</a>
Stacks in computing architectures are regions of memory where data is added or removed in a last-in-first-out (LIFO) manner. [[2]](#second)

## <a name="heap">Heap</a>
Heap is an area of memory for dynamic memory allocation. [[3]](#third)

## <a name="os">Operating System</a>
Operating System manages all things that enable works for a machine. The input device(mouse and keyboard), storing(disk, register, and memory), and calculator(CPU), all types of low-level things are under the control of the operating system. Familiar examples are Windows, Mac, or Linux. 

An operating system (OS) is system software that manages computer hardware, software resources, and provides common services for computer programs. [[4]](#fourth)

## <a name="malloc">malloc</a>
The malloc is a function name in C/C++ to allocate dynamic memory. 

Allocates a block of size bytes of memory, returning a pointer to the beginning of the block. [[5]](#fifth)

## <a name="stack-overflow">Stack overflow</a>
A stack overflow is a programming error when too much memory is used on the call stack. [[6]](#sixth)

## <a name="memory-leak">Memory leak</a>
In computer science, a memory leak is a type of resource leak that occurs when a computer program incorrectly manages memory allocations[1] in a way that memory which is no longer needed is not released. [[7]](#seventh)

## <a name="smart-pointer">Smart Pointer</a>
Smart pointers are used to make sure that an object is deleted if it is no longer used (referenced). [[8]](#eighth)


# Reference
<a name="first">[1]</a> [https://www.udemy.com/course/rust-fundamentals/](https://www.udemy.com/course/rust-fundamentals/)

<a name="second">[2]</a> [https://en.wikipedia.org/wiki/Stack-based_memory_allocation](https://en.wikipedia.org/wiki/Stack-based_memory_allocation)

<a name="third">[3]</a> [https://en.wikipedia.org/wiki/Memory_management#HEAP](https://en.wikipedia.org/wiki/Memory_management#HEAP)

<a name="fourth">[4]</a> [https://en.wikipedia.org/wiki/Operating_system](https://en.wikipedia.org/wiki/Operating_system)

<a name="fifth">[5]</a> [http://www.cplusplus.com/reference/cstdlib/malloc/](http://www.cplusplus.com/reference/cstdlib/malloc/)

<a name="sixth">[6]</a> [https://en.wikipedia.org/wiki/Stack_overflow_(disambiguation)](https://en.wikipedia.org/wiki/Stack_overflow_(disambiguation))

<a name="seventh">[7]</a> [https://en.wikipedia.org/wiki/Memory_leak](https://en.wikipedia.org/wiki/Memory_leak)

<a name="eightn">[8]</a> [https://en.cppreference.com/book/intro/smart_pointers](https://en.cppreference.com/book/intro/smart_pointers)

<a name="ninth">[9]</a> [https://stackoverflow.com/questions/55553048/is-it-possible-to-cause-a-memory-leak-in-rust](https://stackoverflow.com/questions/55553048/is-it-possible-to-cause-a-memory-leak-in-rust)