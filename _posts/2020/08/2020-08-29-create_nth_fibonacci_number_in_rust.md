---
title: "Create the nth Finbonacci Number in Rust"
excerpt: "From the installation to run the code"
toc: true
toc_sticky: true
published: true

categories:
    - Rust
tags:
    - Rust
    - Tutorial
last_modified_at: 2020-08-29T08:06:00-05:00
---

### Why Rust?

"Rust was voted for the fifth year straight the most-loved programming language by developers in Stack Overflow's 2020 survey." [1] 

It seems pretty interesting to start looking at what happens in the Rust world. Besides, one of my colleagues mentioned Rust with [Web Assembly](https://webassembly.org/). I heard that some heavy applications can run in the web browser with Web Assembly such as games. 

"WebAssembly (abbreviated Wasm) is a binary instruction format for a stack-based virtual machine. Wasm is designed as a portable compilation target for programming languages, enabling deployment on the web for client and server applications."[2]

### Philosophy of the Rust

"Rust is a multi-paradigm programming language focused on performance and safety, especially safe concurrency. Rust is syntactically similar to C++, and provides memory safety without using garbage collection." [3]

### Impression from now on

In the middle of the learning step, I feel the compiler is too sweet because the error message is tailored. When I see the detailed error message on the console, I can exactly point out where I did mistakes. I think that makes me feel more productive. I'm not having the benefits of safe types and concurrency yet. 

![example of error message in Rust](/assets/images/2020-08-29/error_msg_in_rust.png)

Presenting one picture is better than thousands of words in this case. The image is from the official documents. [4] What's the error in this case? 

The error tells you exactly what to be changed. The "six" in the else block needs to be changed into integer value because of the if block. Even in the baby learning step, I understand why the language draws so much attentions. 

Here, let's build a simple project that generates the Fibonacci number suggested in the official documentation. [4]

### Install Rust

The first step is installation. [5] For Linux or Mac user, it's one line in the terminal. 

$ curl --proto '=https' --tlsv1.2 [https://sh.rustup.rs](https://sh.rustup.rs/) -sSf | sh

To check after the installation, we can use this line. 

$ rustc --version

Rust provides offline documents. 

$ rustup doc 

### Power of Cargo

We can build, run, and check the code with 'Cargo' and even package management is done by Cargo. How do we start with a new Rust project? 

$ cargo new your_project_name 

How do we build? 

$ cargo build target_project_name 

How do we guarantee that my code is ok? 

$ cargo check target_project_name 

### Create a project

Let's start by creating a new project with cargo. Make sure you are in the right directory. 

$ cargo new fibonacci 

This line will create a new directory. 

![Tree command for project](/assets/images/2020-08-29/fibonacci_project.png)

'fibonacci' is a project directory. In the 'src' folder, we can find our source code and the [main.rs](http://main.rs) is the starting point of all Rust programs. When we start with cargo, the cargo creates a boilerplate hello world program. 

When we print out what's in 'Cargo.toml', we can check out version, author, name, and dependencies. 

Let's run this program with this line. 

$ cd fibonacci 

$ cargo run

![Run in debug mode](/assets/images/2020-08-29/run_in_dev.png)

Finished in 'dev' mode. If we want to run it with optimized release mode, we need to add —release option. 

$ cargo run —release 

![Run in release mode](/assets/images/2020-08-29/run_in_release.png)

### Default Hello World

Please open the src/main.rs file on your favorite editor. I use visual studio code right now. 

```rust
fn main() {
    println!("Hello, world!");
}
```

At the very beginning, we can check out the default code made by cargo. This main function (fn) is the beginning of all Rust programs just like what C does. 

'println!' is a macro function and I do not touch the macro section yet. But according to the above result, we know that print string in the console. The string type is expressed by double quotes (") and the line ends with ';'.  

Before write producing Fibonacci number, let's think about what we need. I guess we need a digit in which the nth number of Fibonacci will be produced. How to get input from the user?

### Get user input

```rust
use std::io;

fn main() {
    let mut nth = String::new();

    io::stdin()
        .read_line(&mut nth)
        .expect("Failed to read line");

    let nth: u32 = nth.trim().parse().expect("Please type a number!");

    println!("Your input is: {}", nth);
}
```

These lines of code will get the number and show you back. 

The first line is import as in Python or #include in C or C++ which means import std::io library. If we use std alone, then we need to write std::io::stdin() in the next line. 

The 'let' is for creating a variable and in this case, we want to store a String object with a new expression which means empty string object. And one more thing here the 'mut'. In Rust, all variables are immutable by default. If we want to change the value of the variable, then we need to specify with 'mut'. Let's keep in mind that the philosophy of Rust; safety and safe concurrency. 

Next, the program will call 'stdin' function in the io module. Also, 'read_line' function will be called right after. What the 'read_line' do is reading input from stdin(standard input). The arguments look so strange for me at first and now I get it. Variables are immutable by default and so does for References. Because references are immutable we need to add 'mut' keyword to change. The reference is the address of a variable which is called Pointer.

"A pointer is a variable whose value is the address of another variable, i.e., direct address of the memory location. Like any variable or constant, you must declare a pointer before using it to store any variable address." [6]

Calling of the 'expect' function will follow. Let's keep remember that the philosophy of Rust; safety. The 'read_line' function returns Result type which contains 'Ok' or 'Err'. When we meet Failure, the 'expect' function will take over the execution flow and the program will be panic. 

Ok, one quite heavy part passed. We create 'nth' again. This is a shadowing. We can't access the first string type 'nth' after shadowing the variable. We annotate its type u32 which means unsigned 32bits integer. 

The 'trim' function will cut out white space from the 'nth' variable. And, 'parse' function transform string to an integer. Finally, the 'expect' function works as explained. 

In the arguments of the 'println!' we can see an empty curly bracket which is a placeholder. In the console, we can see this line. Let's imagine we type 5 and push the enter button. 

Your input is 5.

### Fibonacci project

I think I didn't explain what the Fibonacci is. "Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1." [7]

We now understand how to get an user input and next the main logic. 

```rust
if nth == 0 {
    println!("{} th number of fibonacci is: {}", nth, 0);
} else if nth == 1 {
    println!("{} th number of fibonacci is: {}", nth, 1);
} else {
    let mut _fibo1 = 0; 
    let mut _fibo2 = 1; 
    
    while nth > 1 {
        let next: u32 = _fibo1 + _fibo2;
        _fibo1 = _fibo2; 
        _fibo2 = next; 
        nth -= 1;
    }

    println!("{} th number of fibonacci is: {}", 
            nth, _fibo2);
}
```

I delete the front part of the source code since it's getting too long. I will attach the whole source code in the end. The Fibonacci sequence looks like this line. To make further validation, I used this calculator. [8] The index starts from 0. So 0th Fibonacci number is 0, 1th is 1, 2th is 1, and so on. 

0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...

The code starts with if statement to cover all cases. Inside of the else block, I used the '_fibo1' name as 'fibo1'. When I compile the program, the compiler warns about the name of it. So I added '_' in front of the name. 

In the code, I used while statement to calculate an nth Fibonacci number. That's not interesting but what is interesting happens here. 

When we input to find the 100th Fibonacci number, I got this. 

![Run the n-th Fibonacci in dev](/assets/images/2020-08-29/run_fibo_in_dev.png)

When I run it with 'dev', the debug mode, I got this overflow error. But not in with —release flag. 

![Run the n-th Fibonacci in release](/assets/images/2020-08-29/run_fibo_in_rel.png)

The calculator value is 354,224,848,179,261,915,075 by [8]. What a huge number! In the release mode, it seems like wrapping the value. I mean the program hits the maximum number of the u32 variable and back to 0. 

### How to detect the overflow when we add two values?

This question was given to me during a backend position interview. Wrapping the value makes some strange behavior. Let's imagine that we have a large size of the array. We select two random indexes. We want to use the sum of two indexes as a new index number. Unfortunately, we choose very large numbers (INT_MAX - 2 and INT_MAX - 3) and the program stopped because of the negative index. 

According to the [9] article, there are two methods. 

Method 1 check the sign bits. If two values that have the same sign and the result of summation has a different sign, then overflow is detected. 

Method 2, before the sum of two values, check the integer maximum or minimum. 

### Final thoughts

I care about my productivity and it depends on the tools and language. As a software engineer, we need to use the best tool and Rust shows me clever warning or error messages. That makes me feel more productive. I'm in the baby step for learning the whole concept of Rust. I want to write something that I feel I know to check my understanding. 

```rust
use std::io;

fn main() {
    let mut nth = String::new();

    io::stdin()
        .read_line(&mut nth)
        .expect("Failed to read line");

    let mut nth: u32 = nth
                        .trim()
                        .parse()
                        .expect("Please type positive number!");

    println!("Your input is: {}", nth);

    if nth == 0 {
        println!("{} th number of fibonacci is: {}", nth, 0);
    } else if nth == 1 {
        println!("{} th number of fibonacci is: {}", nth, 1);
    } else {
        let mut _fibo1 = 0; 
        let mut _fibo2 = 1; 
        
        while nth > 1 {
            let next: u32 = _fibo1 + _fibo2;
            _fibo1 = _fibo2; 
            _fibo2 = next; 
            nth -= 1;
        }

        println!("{} th number of fibonacci is: {}", 
                nth, _fibo2);
    }
}
```

### Reference

[1] [Rust was voted for the,actually use it for programming](https://www.zdnet.com/article/programming-languages-rust-enters-top-20-popularity-rankings-for-the-first-time/#:~:text=Rust%20was%20voted%20for%20the,actually%20use%20it%20for%20programming).

[2] [Web Assembly](https://webassembly.org/)

[3] [Philosophy of Rust from wikipedia](https://en.wikipedia.org/wiki/Rust_(programming_language)#:~:text=Rust%20is%20a%20multi%2Dparadigm,safety%20without%20using%20garbage%20collection).

[4] [Rust Error message in the Official Documents](https://doc.rust-lang.org/book/ch03-05-control-flow.html#using-if-in-a-let-statement)

[5] [How to install Rust in Official docs](https://doc.rust-lang.org/book/ch01-01-installation.html)

[6] [Pointer](https://www.tutorialspoint.com/cprogramming/c_pointers.htm#:~:text=A%20pointer%20is%20a%20variable,to%20store%20any%20variable%20address)

[7] [Fibonacci number in wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)

[8] [Fibonacci number calculator](https://keisan.casio.com/exec/system/1180573404)

[9] [Check for the integer overflow](https://www.geeksforgeeks.org/check-for-integer-overflow/)