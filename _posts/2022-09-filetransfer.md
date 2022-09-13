---
title: "File Transfer"
date: 2022-08-19
categories: coding 
tags: [ "coding", "rust", "file" ]
---

# filetransfer

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

<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/748203657?h=9ee10841e9&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="0910(1).mp4"></iframe></div>

The progress bar is based on the file size of the file, displaying the bytes and time elapsed precise.

## File limit

This file trasnfer has **no** size limit, since we split the bytes into multiple buffers gaining the best speed and the less stress on the ram.