---
title: "How to get i-th character from String in Rust"
excerpt: "UTF-8 is the default encoding and it has variational length."
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2020/12/27/rust_string.png
  image: /assets/images/2020/12/27/rust_string.png
  caption: "Photo by me"
  og_image: /assets/images/2020/12/27/rust_string.png

categories:
    - Rust
tags:
    - Rust
last_modified_at: 2020-12-27T08:06:00-05:00
---

# Intro
```rust
fn main() {
  let string = String::from("127.0.0.1:8080"); 
  let string_slice = &string[10..]; 
  let string_borrow: &str = &string; 
  let string_literal = "1234"; 

  dbg!(&string); 
  dbg!(string_slice); 
  dbg!(string_borrow); 
  dbg!(string_literal);
}
```
This code shows this result. 
```
[src/main.rs:11] &string = "127.0.0.1:8080"
[src/main.rs:12] string_slice = "8080"
[src/main.rs:13] string_borrow = "127.0.0.1:8080"
[src/main.rs:14] string_literal = "1234"
```

Accessing the characters by using the direct index is dangerous since we have no idea how much space is required to store string data. We can say string without what the type of a string will be. The string data is quite complex to store machine-friendly way. All characters are translated into the digital way; numbers. Fundamentally, it should be represented by combining multiple zeros and ones. 

# Encoding
How to do that? With a code map, we can call it encoding scheme; [ASCII](#ascii), [UTF-8](#utf_8), and [Unicode](#unicode). In the table of those encoding system, we can find some examples of characters. Common English letters have the same value. Since the encoding map is growing with developing computer memory, the successor should keep the rule. Here's an interesting post about encoding[[4]](#fourth); ASCII, Unicode, UTF-8, and UTF-16. 

# In Rust 
```rust
fn main() {
    let eng = "f";
    let emoji = "🔥";
    println!("{:?} {}", eng, emoji);
}
```
Let me use the [debugger](#fifth) to see what's going on. 
![result](/assets/images/2020/12/27/rust_string.png)

The debugger tells us about how to store string type data in memory. We need to catch each digit number index (a direct index) represent 1 byte. The "emoji" variable shows how to store the fire emoji. The first index is 0. In the 0, '\xf0' is stored. It is a [hexadecimal](#hexadecimal) expression to show the raw binary value(11110000). The length is 8. We need 8 bits to store the value(11110000). For the fire emoji, if we try to access it directly, the Rust compiler shows an error. How to do it in Rust?
![result](/assets/images/2020/12/27/rust_string_2.png)

# Rust access n-th character
As suggested in the error message, we are going to call chars().nth() method and also bytes().nth().
```rust
fn main() {
    let eng = "f";
    let emoji = "🔥";
    println!("{:?} {}", eng, emoji.chars().nth(0).unwrap());

    println!("{:?} {}", eng, emoji.bytes().nth(0).unwrap());
}
```

```
"f" 🔥
"f" 240
```
The 'chars' and 'nth' is not far away from the main idea. But what 'unwrap' mean? Rust has no null value. To handle this, Rust introduces 'Some' type that can represent an absence of value. The 'unwrap' consuming the value in it or panic. So, its use is generally discouraged. [[7]](#seventh) 

Here is the code to print the 'Some' type. 
```rust
fn main() {
    let eng = "f";
    let emoji = "🔥";
    println!("{:?} {:?}", eng, emoji.chars().nth(0));

    println!("{:?} {:?}", eng, emoji.bytes().nth(0));
}
```

```
"f" Some('🔥')
"f" Some(240)
```


# Terms
## <a name="ascii">ASCII</a>
ASCII abbreviated from American Standard Code for Information Interchange, is a character encoding standard for electronic communication. [[1]](#first)

## <a name="utf_8">UTF-8</a>
UTF-8 is a variable-width character encoding used for electronic communication. Defined by the Unicode Standard, the name is derived from Unicode (or Universal Coded Character Set) Transformation Format – 8-bit. [[2]](#second)

## <a name="unicode">Unicode</a>
Unicode is an information technology (IT) standard for the consistent encoding, representation, and handling of text expressed in most of the world's writing systems. [[3]](#third)

## <a name="hexadecimal">Hexadecimal</a>
In mathematics and computing, the hexadecimal (also base 16 or hex) numeral system is a positional numeral system that represents numbers using a radix (base) of 16. [[6]](#sixth)

# References
<a name="first">[1]</a> [https://en.wikipedia.org/wiki/ASCII](https://en.wikipedia.org/wiki/ASCII)

<a name="second">[2]</a> [https://en.wikipedia.org/wiki/UTF-8](https://en.wikipedia.org/wiki/UTF-8)

<a name="third">[3]</a> [https://en.wikipedia.org/wiki/Unicode](https://en.wikipedia.org/wiki/Unicode)

<a name="fourth">[4]</a> [https://medium.com/@apiltamang/unicode-utf-8-and-ascii-encodings-made-easy-5bfbe3a1c45a](https://medium.com/@apiltamang/unicode-utf-8-and-ascii-encodings-made-easy-5bfbe3a1c45a)

<a name="fifth">[5]</a> [https://devjunhong.github.io/rust/Rust-step-by-step-debugger/](https://devjunhong.github.io/rust/Rust-step-by-step-debugger/)

<a name="sixth">[6]</a> [https://en.wikipedia.org/wiki/Hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal)

<a name="seventh">[7]</a> [https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap)
