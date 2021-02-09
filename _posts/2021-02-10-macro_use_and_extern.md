---
title: "macro_use and extern crate"
excerpt: "bash command can save your time"
toc: true
toc_sticky: true
published: true
header:
  # teaser: /assets/images/2021/02/06/soft_skills_v2.jpeg
  # image: /assets/images/2021/02/06/soft_skills_v2.jpeg
  # caption: "Photo by me"
  # og_image: /assets/images/2021/02/06/soft_skills_v2.jpeg
layout: single
# classes: wide

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2021-02-10T08:06:00-05:00
---

```rust
#[macro_use]
extern crate diesel;
```

I find this snippet of code in the [diesel tutorial document](http://diesel.rs/guides/getting-started/). What is the "macro_use" attribute? What does it mean "extern crate"?

# macro_use 
The first thing I noticed is this statement is always one line up of the "extern crate" statement. These lines of code is used like a pair.

The attribute imports macros in the crates. For example, the above snippet means, in this scope, we can use macros that are defined in diesel crates. 

[Answer from Stackoverflow](https://stackoverflow.com/a/54954792/5742992)

# extern crate
In a nutshell, it is equivalent to the "use" statement. It indicates that you want to link against an external library and brings the top-level crate name into scope. 

[Answer from Stackoverflow](https://stackoverflow.com/a/29404692/5742992)

# Updated 
```rust
#[macro_use]
extern crate diesel;
```

If you are working under the recent version of Rust, then you don't have to follow the old custom. We can use the "use" statement to achieve both. For my environment, I use 1.48.0 and it does not have a problem. 

```rust
use diesel;
```
