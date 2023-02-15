---
title: "Integrating Rust Rocket and React"
excerpt: "Using Cargo and create-react-app from scratch"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/02/rust_rocket_react.png
  image: /assets/images/2021/01/02/rust_rocket_react.png
  caption: "Photo by me"
  og_image: /assets/images/2021/01/02/rust_rocket_react.png
# layout: single
# classes: wide

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2021-01-02T08:06:00-05:00
---

# Intro
After I took a course from Udemy, I want to check my understanding of Rust using multiple approaches. The first is [reading the source code and explain how it works](https://devjunhong.github.io/rust/lets-not-build-a-server/). The second one is creating a real-life app using Rust. By using API or crawling, checking the air quality in Seoul and sending it to my email every 8 a.m.  After the Covid-19, all kinds of the indoor fitness center are shutting down. I want to keep work out. The simple way is that I can run. Usually, before going out, I check the air quality and I get the idea of the automation. To build an app, I want to build using Rust Rocket as a backend and React as a frontend. Here is the starting point that setting up integrating Rust rocket and React. 

# Repository 
[https://github.com/devjunhong/rust_rocket_and_react](https://github.com/devjunhong/rust_rocket_and_react)

# Dependency 
* Rust: rustc 1.50.0-nightly
* Rust Rocket: 0.4.6
* Cargo: 1.50.0-nightly
* npm version: 6.14.10
* create-react-app: 4.0.1

# Create Rust Rocket Backend
```bash
$ cargo new backend
```
Creating a new Rust project is the first step. With this command, we can make the "backend" project. 

## Updating Cargo.toml 
Since we are choosing [Rocket](https://rocket.rs/) as the backend, we are going to add the dependency project information into the "backend/Cargo.toml" file.

```toml
[dependencies]
rocket = "0.4.6"
```

## Compiler Setting 
Rocket requires a nightly version of Rust. We need to make sure the rust compiler version.
```bash
$ rustup --version 
```
To set the Rust compiler per-directory, we can use this command.
```bash
$ rustup override set nightly
```

## Add sample code to the main.rs
```rust
#![feature(proc_macro_hygiene, decl_macro)]

#[macro_use] extern crate rocket; 

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

fn main() {
    rocket::ignite().mount("/", routes![index]).launch();
}
```
The sample code is from Rocket documentation [[3]](#third). From this point, we can use this command to launch the Rocket server. The current working directory is under the "backend/". The full path is "/path/to/backend/". In the console, 
```bash
$ cargo run 
```
Then, we enter the address printed in the console with your browser. We will see. Okay, the backend project works now.
![hello_world_image](/assets/images/2021/01/02/hello_world.png)

# Create React frontend
```bash
$ create-react-app frontend
```
In the many tutorials, we can run the react app by hitting "npm run start". Here was the strange point that I feel something missing. I have no idea how to run it locally without a server. This article shed light on. [[1]](#first) Here's the following.

## Setting up package.json 
```json
{
  "name": "frontend",
  "version": "0.1.0",
  "homepage": "."
}
```
Adding the "homepage" key with the value "." means the build output of index.html will point to the current "build" directory. The "index.html" finds its resource from the "build" directory. Concretely, it's not the "index.html", the browser. 

```bash
$ npm run build
```
I can find a new directory under t"frontend" folder. "build". Inside of it, we have "index.html". Drawing the index.html(frontend/build/index.html) file on the browser, we can see the local react app. It's time to integrate both. 

![local_image](/assets/images/2021/01/02/local_react.png)

# Integrate Backend and Frontend
Let's make sure what's left. The backend server only knows the root access. The frontend project successfully creates "index.html". Okay, if there's root access again, then we need to point the "frontend/build/index.html" file. Go for it, we need to update "backend/src/main.rs". 

## Update backend/src/main.rs
```rust
use std::path::Path; 
use rocket::response::NamedFile;

#[get("/")]
fn index() -> io::Result<NamedFile> {
  let page_directory_path = 
  format!("{}/../frontend/build", env!("CARGO_MANIFEST_DIR"));
  NamedFile::open(Path::new(&page_directory_path).join("index.html"))
}
```
The format macro and env macro are discussed [here](https://devjunhong.github.io/rust/lets-not-build-a-server/#main-function). The value of the "page_directory_path" variable is "/path/to/the/backend/../frontend/build". That's pointing "/path/to/the/frontend/build". And the path will be combined with "index.html" by calling the join function. 
```rust
Path::new(&page_directory_path).join("index.html")
```
This code points to the "/path/to/the/frontend/build/index.html" file. The open function read file in read-only mode. This is for the root path. If we have additional resources, then we need to route those too. To serve additional files, we need to create another function.

```rust
#[get("/<file..>")]
fn files(file: PathBuf) -> io::Result<NamedFile> {
  let page_directory_path = 
  format!("{}/../frontend/build", env!("CARGO_MANIFEST_DIR"));
  NamedFile::open(Path::new(&page_directory_path).join(file))
}
```
The get attribute should be mentioned first. [[4]](#fourth) To match with multiple elements, we use dot-dot("..") operation. When the browser requests "http://localhost:8000/static/main.css", the last part of the string ("static/main.css") is the value of the "file" argument. The "page_directory_path" variable is what we've seen before. The same one. The value of it is "/path/to/the/frontend/build". The pieces of the puzzle are complete. It is ready to serve CSS or JS files to make our page beautiful. I got idea from this repository.[[2]](#second) Thank you.

## Path Traversal Attack 
According to [[4]](#fourth), Rocket prevents the [path traversal attack](#path_traversal_attack). If we can upper-level directory or file that is not allowed to be disclosed, we can see any information from the server. To test, we need to run the server first. And, we are going to use the [curl](#curl) command.  
```bash
$ curl localhost:8000/
```
By using another console screen, we can enter the command. As expected, I see the exact source code when I enter the address (localhost:8000). We create a server. When we send a request, the server points "/path/to/the/frontend/build". Let's try curl request with this argument. "localhost:8000/../package.json". The request means that showing the "/path/to/the/frontend/package.json" file. The message I got is 500 Internal Server Error. 

# Outro
In this post, we have a look at how to integrate Rust Rocket and react. It was interesting for me to check understandings and make it firm as well. I stucked on creating a react app without a server. And, I found this article [[1]](#first). It points out that we should understand favorite tools about what's happening or what's going on. I totally agree on this idea. Trying to describe the practical steps, I felt the missing things. This is why I write blog posts. Thank you. Any questions are welcome in the replies or reactions too. We can learn together. 

# Terms
* <a name="path_traversal_attack">Path Traversal Attack</a>

A directory traversal (or path traversal) attack exploits insufficient security validation or sanitization of user-supplied file names, such that characters representing "traverse to parent directory" are passed through to the operating system's file system API. [[5]](#fifth)

* <a name="curl"> curl </a>

cURL (pronounced 'curl'[4]) is a computer software project providing a library (libcurl) and command-line tool (curl) for transferring data using various network protocols. [[6]](#sixth)

# References
<a name="first">[1]</a> [https://medium.com/@louis.raymond/why-cant-i-open-my-react-app-by-clicking-index-html-d1778f6324cf](https://medium.com/@louis.raymond/why-cant-i-open-my-react-app-by-clicking-index-html-d1778f6324cf)

<a name="second">[2]</a> [https://github.com/StefanoOrdine/rust-reactjs](https://github.com/StefanoOrdine/rust-reactjs)

<a name="third">[3]</a> [https://rocket.rs/v0.4/guide/getting-started/#hello-world](https://rocket.rs/v0.4/guide/getting-started/#hello-world)

<a name="fourth">[4]</a> [https://rocket.rs/v0.4/guide/requests/#multiple-segments](https://rocket.rs/v0.4/guide/requests/#multiple-segments)

<a name="fifth">[5]</a> [https://en.wikipedia.org/wiki/Directory_traversal_attack](https://en.wikipedia.org/wiki/Directory_traversal_attack)

<a name="sixth">[6]</a> [https://en.wikipedia.org/wiki/CURL](https://en.wikipedia.org/wiki/CURL)