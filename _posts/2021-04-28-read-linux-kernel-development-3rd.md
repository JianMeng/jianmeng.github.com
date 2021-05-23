---
title: "read linux kernel development 3rd"
permalink: blog/poka-yoke-update-firmware.html
layout: post
fuzzydate: April 2021
---

Recently I almost spent 4 months time to read linux kernel development book which writed by Robert Love. It is a third edition tranlated to Chinese, which I borrowed from local library. I found it from college library 19 years ago, at that time it is a twice edition. But I don't read that red cover edition. But I always want to need more details about how OS is work. So I start to read it now since I have more time now.

The process is a bit zigzag, as my method is trying to more every corner of each function that appear in book. So reading code took a lot of time, especially red black tree part. It make me read a few chapters from another algorithm book. As I read more, I realize linux is whole piece work. Each component is close related another. Therefor, a quick view from top side of mountain is important. You need have a general landscape about it, then drill into the part interesting. 

A strange part about linux related book is that those book try to teach what is this operation system as primary intent. Then it start from what is process and how to schedule them. This book is not an exception. The problem of this approach is that it put the software structure in reversing order. I mean, the "bore" thing, such as gcc related specail usage, pointer, list and rb-tree, should be put in first place. They compose the software structure. They are the underlaying fundamental. All thing is built upon them. This is especially true a book is call itself an introduce to linux code. It encourage people read code. After finish one chapter, i read the related code only found lose myself in underlaying fundamental. A lot of time-wasting google thing happens there. When I read the later chapter 6, kernel data structure, I found what I need to frist know is all in it. The author must kid me. (⊙o⊙)…

What I expect from is this book is to explain the lock implement in operation system. Not the api to call, but how to use hardware to implement it. 


It is a good book. It help me understand a lot detail command in linux how they work. You shoud read it.