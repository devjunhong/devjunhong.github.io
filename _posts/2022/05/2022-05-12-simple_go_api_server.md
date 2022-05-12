---
title: "Basic API with Golang"
excerpt: "Develop the very basic API with Golang"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2022/05/go_api_postman.png
  # image: /assets/images/2022/04/range_python.png
  # caption: "Photo by [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/python?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  
  og_image: /assets/images/2022/05/go_api_postman.png
layout: single
# classes: wide
word-wrap: break-word;
categories:
    - Go
tags:
    - Go
last_modified_at: 2022-05-12T06:43:00-05:00
---

[Go](https://go.dev/) and [Rust](https://www.rust-lang.org/) are new languages compared with other big names; C/C++ or Java. Personally, Go lang and Rust lang doesn't compete each other. I belive they will go together since their purposes are different. Go is standing for the simplist approach. It can be easily picked by C/C++ or Java developers. Rust chooses a strict way in terms of managing low level control. Rust will be adapted in more critical situation and if they want to drop the last performance. Oneday I want to try Golang. Today is the day. In this posting, I'd like to show how I build a "hello" api server with Golang. The code is [here](#code). 

# Basic mechanism of HTTP web server 

A server is responding to user's request. We've faced 404 errors that means the request not found with the given address. That's quite common error that many cool companies are working on in terms of design. 

![github 404](/assets/images/2022/05/github_404.png)

Errors starts with "4" (4xx) represents usually user's fault and starts with "5" (5xx) means server side faults. There are two kinds of server we can make. 

## Static Server 
A server only replies to the fixed format/template of the response. It doesn't involve with processing and keep the state of user request. This blog is created by jekyll static site generator. The blog is on top of the well known theme; [minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/)

## Dynamic Server
The dynamic server accepts request and processes. Sometimes it keeps the information. The infromation we keep is called as a "state". Usually, we use Databases for keeping the state. 

In terms of networking each other, we use HTTP protocol. It's a promise of communication method. 

# Handler and Router 
Let's imagine whe we type `http://127.0.0.1:8080/hello` url on the browser. 

The server instance will accept the request and find the request based on the url. In this case, server (http://127.0.0.1:8080) makes a decision to respond `hello` path. The address we can use is the routing and each routing has it's own handler function. The server developer can make various features based on the routing. 

To implement routing in action, we have multiple ways with golang. This [article](https://benhoyt.com/writings/go-routing/) nicely covered about the routing topic. 

1. Regex table - Loop through pre-compiled regexes and pass matches using the request context
2. Regex switch - A switch statement with cases that call a regex-based match() helper which scans path parameters into variables
3. Pattern matcher - Similar to the above, but using a simple pattern matching function instead of regexes
4. Split switch - Split the path on / and then switch on the contents of the path segments
5. Shift path - Axel Wagner's hierarchical ShiftPath technique
6. Library, Chi 
7. Library, Gorilla
8. Libaray, Pat

# HTTP request and response headers 
In the HTTP protocol, it's already defined what we need to fill in for the request and response headers. Which type of request it should be, authentication credentials, control for caching, or to get information about the user agent or referrer. 

# Marshaling data structures to JSON
"Marshaling" in this context means converting memory representation (byte stream) to the JSON object. 

# <a name="code">TLDR; Code</a>
So far, we've built up necessary details for building a simple server. I used "gorilla" for routing function. 

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"

	"github.com/gorilla/mux"
)

type Person struct {
	Name string `json:"name"`
}

func main() {
	r := mux.NewRouter()

	r.HandleFunc("/", rootHandler)  // handler 

	http.ListenAndServe(":80", r)  // start server with a router
}

func rootHandler(w http.ResponseWriter, r *http.Request) {
	var p Person

	err := json.NewDecoder(r.Body).Decode(&p)  // marshaling
	if err != nil {
		http.Error(w, err.Error(), http.StatusBadRequest)
		return
	}

	fmt.Fprintf(w, "Hey "+p.Name) // response 
}
```

The prerequisit to run this code is to install the [golang](https://go.dev/dl/) within your local device. Then, create a go file with this code; `main.go` and try `go run main.go`.

Using the Postman, you can test your server with this body. `{"name": "your name"}`

Here I only have the root routing. The example response is here. 

![postman response](/assets/images/2022/05/go_api_postman.png)

# Reference 
* [Mechanism of web server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)
* [Routing in Golang](https://benhoyt.com/writings/go-routing/)
* [Request header](https://developer.mozilla.org/en-US/docs/Glossary/Request_header)
* [Response header](https://developer.mozilla.org/en-US/docs/Glossary/Response_header)