---
title: "File Transfer"
date: 2022-08-19
categories: coding 
tags: [ "coding", "rust", "file" ]
---

I've been working on this project for 1 week, this is a filetrasnfer i made with a friend, it's written in rust, i'd like to show you how it works and why it's the fastest ever.

## Speed

This program is written in **rust**, its performance are extremely efficent and fast, its memory managment is insane, it doesn't have a garbage collector neither a runtime,
its compiler is incredibly smart, that's mainly why this file trasnfer is one of the fastest ever.

## Multithread

This file transfer supports multithreading using `std::thread` for each established connection, this really helps in terms of perfomance and gives the possibility to send **multiple files** at the same time, which is really helpful.


## Metadata and serialization

When sending a file in a buffer of bytes, we allocate to the buffer 4kb for the metadata managed by a struct.

```rust
#[derive(serde::Serialize, serde::Deserialize)]  
struct Metadata {  
    file_size: u64,  
    file_name: String,  
    file_extension: String,  
}
```

The metadata is serialized in json, and deserialized by the receiver that reads the data from the json. This is a choice we made to have a cleaner and more organized code.

## Connection

For the connection we use the standard and fastest library for TCP connection `std::net`, in particular `TcpStream` and `TcpListener`,
this allows the file trasnfer to make a safe and fast connection.

## Progress bar

<iframe width="800" height="600" src="https://www.youtube.com/embed/v4_hRdEC7Fo" title="preview" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The progress bar is based on the file size of the file, displaying the bytes and time elapsed precise.

## File limit

This file trasnfer has **no** size limit, since we split the bytes into multiple buffers gaining the best speed and the less stress on the ram.
