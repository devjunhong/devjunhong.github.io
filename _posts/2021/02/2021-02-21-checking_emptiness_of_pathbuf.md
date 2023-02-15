---
title: "Checking emptiness of PathBuf variable"
excerpt: ""
# toc: true
# toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/02/21/programming.jpg
  # image: /assets/images/2021/02/06/soft_skills_v2.jpeg
  caption: "Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  # og_image: /assets/images/2021/02/06/soft_skills_v2.jpeg
layout: single
# classes: wide

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2021-02-21T08:06:00-05:00
---

If you are working with a path of a file in Rust such as manipulating the path of a file by appending, the PathBuf type is useful. I want to compare the emptiness of PathBuf data. Here's how to do it. 

```rust
use std::path::PathBuf; 

let mut path = PathBuf::new();

let is_empty: bool = path.as_os_str().is_empty();

println!("{:?}", is_empty);
# true

if is_empty {
  path.push("empty");
} else {
  path.push("not_empty");
}
```

[Here is the issue with the checking emptiness of PathBuf.](https://github.com/rust-lang/rust/issues/30259)


[Here is about PathBuf type in Rust.](https://doc.rust-lang.org/std/path/struct.PathBuf.html)
