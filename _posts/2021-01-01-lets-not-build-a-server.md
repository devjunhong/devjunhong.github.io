---
title: "Let's not build a server from scratch but read source code in Rust"
excerpt: "Read source code and check for my understanding"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/01/rust_server_science.jpg
  image: /assets/images/2021/01/01/rust_server_science.jpg
  caption: "Photo by [Science in HD](https://unsplash.com/@scienceinhd?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/server?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)"
  og_image: /assets/images/2021/01/01/rust_server_science.jpg
layout: single
classes: wide

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2021-01-01T08:06:00-05:00
---

# Intro
I recently took a course [[1]](#first) about Rust. In the Udemy course, I had a chance to build an HTTP server from scratch. By finishing it, I can understand such low-level details of what's going on under the hood. Since I enjoyed it a lot, I'm going to read and explain the code in this repository. [[2]](#second) And, I try not to forget detail by explaining to others. I hope I can test my knowledge by writing this article too. If I cannot deliver a concept, then I probably may not understand it very well. This article will be full of snippets of Rust code. Here is the file structure to help understand. 

![Structure of project](/assets/images/2021/01/01/rust_server_project.png)

## main.rs
The "main.rs" file is a starting point of most Rust project. This file is under the "src" folder. If we can't find the "main.rs" file in the project, we need to check [bin] property specified in "Cargo.toml" file. The full source code for "main.rs" is here. From here, we are going to take a look at partial code.

```rust
#![allow(dead_code)]

use server::Server; 
use website_handler::WebsiteHandler;
use std::env;

mod server;
mod http;
mod website_handler;

fn main() {
    let default_path = format!("{}/public", env!("CARGO_MANIFEST_DIR"));
    let public_path = env::var("PUBLIC_PATH").unwrap_or(default_path);
    println!("public path: {}", public_path);
    let server = Server::new("127.0.0.1:8080".to_string()); 
    server.run(WebsiteHandler::new(public_path)); 
}
```

### allow(dead_code)

```rust
#![allow(dead_code)]
```

The first line makes the compiler does not warn for [dead code](#dead_code). If compiler warnings make you annoying, we can use this attribute. By keeping these warnings, we can have a benefit not to detect dead code by ourselves. 

### use keyword 
```rust
use server::Server;
use std::env;
use website_handler::WebsiteHandler;
```
Those "use" statements bring modules that are declared outside of the "main.rs" file. In Rust, every single file will be treated as a module. The first "use" statement points to the "server.rs" file. In the "server.rs" file, we can check out the "Server" implementation. Next one "std" means standard library in Rust. From the standard library, we need the "env" module. The third one is the same as the server. 

### mod keyword 
```rust
mod http;
mod server;
mod website_handler;
```
The "mod" keyword create new modules or include other modules. [[4]](#fourth) The first mod statement (mod http) means include "http.rs or http/mod.rs". [[5]](#fifth) It is not allowed to have both "http.rs" and "http/mod.rs" at the same time. [[6]](#sixth) The remains of the code will be the same. 

### main function 
```rust
fn main() {
  //...
}
```
The main function is the starting point of all Rust program. If we visit another Rust code base, we can find the main function. 

```rust
let default_path = format!("{}/public", env!("CARGO_MANIFEST_DIR"));
```
The let keyword assigns a new variable. We call the format is a macro in Rust. We can go to the definition of this macro when we hit f12 in the [Visual Studio Code](https://devjunhong.github.io/rust/Rust-step-by-step-debugger/). What format macro does is fill out the square bracket from the given arguments. The "{}/public" will be filled out by the result of env!("CARGO_MANIFEST_DIR"). The env is another macro that retrieves the matching environment variable. The value of "CARGO_MANIFEST_DIR" from the environment variable will be resolved. It means the directory path of "Cargo.toml" file. This is one technique to run the source code in another person's machine. The resolved value will be assigned to the "default_path" variable. 

```rust
let public_path = env::var("PUBLIC_PATH").unwrap_or(default_path);
```
The "env" macro inspects the environment variable in the [compile-time](#compile_time) but the "var" function will do in [run time](#run_time). Since there's no absence of the "PUBLIC_PATH" value, it can fall into null. The "unwrap_or" function returns the value when only it's ok. If the "PUBLIC_PATH" value does not exist, the "default_path" value will be assigned. 

```rust
println!("public path: {}", public_path);
```
According to the above, we call it a macro ("println!"). It will print the given string in the console. As format macro does, this fills up the square bracket with the given arguments. 

```rust
let server = Server::new("127.0.0.1:8080".to_string()); 
```
The "Server::new" means calling the new function under the "Server" module. In this case, we need to check up the matching "use" statement. It's the "use server::Server". For the argument, it converts the string slice type into String type. The String type is stored in the [heap area](https://devjunhong.github.io/rust/about-rust-memory/#heap). We can increase the length of the string. However, the string slice type is one fixed-length type. It's immutable data. [[9]](#nineth) The "new" function instantiate struct and assign it to the "server" variable. 

```rust
server.run(WebsiteHandler::new(public_path)); 
```
We use "server" struct here by calling the "run" function. The "run" function consumes the "WebsiteHandler" struct instantiated by the "public_path".



# Term 
## <a name="dead_code">dead code</a>
Some use the term to refer to code (i.e. instructions in memory) which can never be executed at run-time. In some areas of computer programming, dead code is a section in the source code of a program which is executed but whose result is never used in any other computation. [[3]](#third)

## <a name="compile_time">Compile-time</a>
Compile time refers to the time duration in which the programming code is converted to the machine code (i.e binary code) and usually occurs before runtime. [[7]](#seventh)

## <a name="run_time">run time</a>
In computer science, runtime, run time, or execution time is the final phase of a computer program's life cycle, in which the code is being executed on the computer's central processing unit (CPU) as machine code. [[8]](#eighth)

# References
<a name="first">[1]</a> [https://www.udemy.com/course/rust-fundamentals/](https://www.udemy.com/course/rust-fundamentals/)

<a name="second">[2]</a> [https://github.com/gavadinov/Learn-Rust-by-Building-Real-Applications](https://github.com/gavadinov/Learn-Rust-by-Building-Real-Applications)

<a name="third">[3]</a> [https://en.wikipedia.org/wiki/Dead_code](https://en.wikipedia.org/wiki/Dead_code)

<a name="fourth">[4]</a> [https://doc.rust-lang.org/std/keyword.mod.html](https://doc.rust-lang.org/std/keyword.mod.html)

<a name="fifth">[5]</a> [https://doc.rust-lang.org/rust-by-example/mod/split.html](https://doc.rust-lang.org/rust-by-example/mod/split.html)

<a name="sixth">[6]</a> [https://doc.rust-lang.org/reference/items/modules.html#module-source-filenames](https://doc.rust-lang.org/reference/items/modules.html#module-source-filenames)

<a name="seventh">[7]</a> [https://en.wikipedia.org/wiki/Compile_time](https://en.wikipedia.org/wiki/Compile_time)

<a name="eighth">[8]</a> [https://en.wikipedia.org/wiki/Runtime_(program_lifecycle_phase)](https://en.wikipedia.org/wiki/Runtime_(program_lifecycle_phase))

<a name="nineth">[9]</a> [https://stackoverflow.com/a/24159933/5742992](https://stackoverflow.com/a/24159933/5742992)