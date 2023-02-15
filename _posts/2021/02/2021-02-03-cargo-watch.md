---
title: "Rust auto reload with cargo watch"
excerpt: "Do not enter cargo run command"
toc: true
toc_sticky: true
published: true
header:
  # teaser: /assets/images/2021/02/03/bias_and_variance.png
#   image: /assets/images/2021/01/24/openface_og_updated.png
#   caption: "Photo by me"
  # og_image: /assets/images/2021/01/31/bias_and_variance.png
layout: single
# classes: wide

categories:
    - Rust
tags:
    - Cargo 
last_modified_at: 2021-02-03T08:06:00-05:00
---

# Nodemon

When I develop a node.js application, I don't enter the run command since there is a [nodemon](https://www.npmjs.com/package/nodemon) that automatically restarting the application when file changes in the directory are detected. The same you can find in Rust is [Cargo Watch](https://docs.rs/crate/cargo-watch/7.0.2).

# cargo-watch

At first, you need to install the cargo-watch using this command. 
```sh 
$ cargo install cargo-watch
```

After the installation is ok, we can run it by hitting this command. 
```sh
$ cargo watch [-x command]...
```

I found this when I read the [actix-web official document](https://actix.rs/docs/autoreload/). It seems that cargo watch applies to every Rust project. 

For the actix-web project, I use this. 

```sh 
$ cargo watch -x run
```