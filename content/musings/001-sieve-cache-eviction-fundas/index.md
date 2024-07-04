---
slug: sieve-cache-eviction
title: "SIEVE: A New Algorithm from CMU Revolutionizes Caching"
date: "2024-07-04"
tags: ["caching", "algorithms"]
summary: "Caching stores copies of webpages or their elements closer to the user for faster access. SIEVE is a novel cache eviction algorithm that efficiently manages cache space by quickly identifying and removing unpopular objects while retaining popular ones, optimizing performance."
description: "SIEVE is a simple yet efficient cache eviction algorithm that enhances performance by quickly identifying and removing unpopular objects while retaining popular ones."
toc: true
readTime: true
math: true
showTags: true
---

This article was originally published on the [May 2024 Edition](https://drive.google.com/file/d/1Zd5ekbe4mL56WQSzfimrzhO88nvELNyz/view)
of the insIIITS Newsletter.

## What is caching ?

Caching in the context of web browsing is like storing a copy of a webpage or its elements (like images, scripts, etc.) closer to you, usually on your device or on servers located nearby. This way, when you revisit the same webpage, your browser can quickly fetch the elements it already has instead of downloading them again from the original server. This speeds up your browsing experience significantly because it reduces the time needed to load webpages. Additionally, caching also lightens the load on internet infrastructure by reducing the number of requests sent to faraway servers, which is crucial for efficient internet use, especially in times of heavy traffic or slow connections.


## Cache Hierarchy

Think of cache hierarchy like a series of shelves for storing books. The shelves closest to you (like your desk or a nearby bookshelf) represent the smaller, faster caches, while shelves further away (like a bookcase in another room) represent larger, slower caches or the main memory.

When you need a book, you first check the shelves closest to you (the smaller caches). If the book is there (meaning it's cached), you grab it quickly. If not, you go to the next shelf further away (larger cache) until you find the book.


## Cache Eviction

Eviction is like when you need space for a new book but all your shelves are full. You have to decide which book to remove to make room for the new one. This decision could be based on how often you use the books or some other rule. Similarly, in computer systems, when a cache is full, it needs to decide which data to remove (evict) to make space for new data.


## LRU

LRU stands for "Least Recently Used." It's a strategy used in caching systems to decide which items to remove (evict) when the cache is full and needs space for new items.

Imagine you have a shelf with several books on it, and you're only allowed to keep a certain number of books at a time. Every time you use a book, you put it at the front of the shelf. When you need to make space for a new book, you remove the book at the back of the shelf because it's the one you haven't used for the longest time.

In computer systems, the "shelf" represents the cache memory, and the "books" represent cached items like data or web pages. When a new item needs to be cached but the cache is full, the LRU algorithm identifies the least recently used item and evicts it to make space for the new one. This ensures that the most recently accessed items are kept in the cache, optimizing performance by prioritizing frequently accessed data.



![Sieve working gif](https://cachemon.github.io/SIEVE-website/assets/images/illustrations/sieve_diagram.gif)

(Source [Sieve Website](https://cachemon.github.io/SIEVE-website/))


## SIEVE

SIEVE, which stands for Simple and Efficient Value-based Eviction, is a novel cache eviction algorithm designed to improve the performance of web caches, such as Content Delivery Networks (CDNs) and key-value caches.

 It was created by a team of experts: Yazhuo Zhang (Emory University), Juncheng Yang (Carnegie Mellon University), Yao Yue (Pelikan Foundation), Ymir Vigfusson (Emory University & Keystrike), and K. V. Rashmi (Carnegie Mellon University). This groundbreaking work is set to be published in the prestigious [USENIX NSDI](https://www.usenix.org/conference/nsdi24) conference proceedings in 2024.

The core idea behind SIEVE is to efficiently manage cache space by quickly identifying and removing unpopular objects while retaining popular ones. Unlike many complex eviction algorithms that trade simplicity for efficiency gains, SIEVE maintains a simple design while achieving remarkable performance improvements.

## How SIEVE Works

The core ideas behind SIEVE's implementation can be summarized in the following points:

1. **Data Structure**: SIEVE utilizes a simple data structure consisting of a single FIFO (First-In-First-Out) queue and a pointer called "hand." The FIFO queue maintains the insertion order of objects, while the hand points to the next eviction candidate in the cache.

2. **Cache Operations**: When an object is accessed, SIEVE marks it as "visited." During a cache miss, SIEVE examines the object pointed to by the hand. If it has been visited, indicating recent usage, SIEVE resets its visited status and moves the hand to the next position. This process continues until an unvisited object is encountered, which is then evicted from the cache.

3. **Lazy Promotion and Quick Demotion**: SIEVE incorporates both lazy promotion and quick demotion strategies. Lazy promotion ensures that objects are promoted only at eviction time, reducing unnecessary overhead. Quick demotion allows SIEVE to swiftly remove newly-inserted, unpopular objects, maintaining cache efficiency.

4. **Scalability and Simplicity**: SIEVE's design eliminates the need for locking during cache hits, enhancing multi-threaded throughput. Moreover, its simplicity allows for easy implementation in various cache libraries with minimal code changes.



![Sieve algorithm](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mpag95nof8cscey2ikoz.png)



*SIEVE is simple and efficient. The code snippet shows how FIFO-*
*Reinsertion and SIEVE find eviction candidates. Minor code changes convert*
*FIFO-Reinsertion to SIEVE, unleashing lower miss ratios than state-of-the-art*
*algorithms.* (Source: SIEVE Paper)

If you wish to get a brief overview of SIEVE, visit their official website https://cachemon.github.io/SIEVE-website/


For the more technically curious guys, you may read the paper https://junchengyang.com/publication/nsdi24-SIEVE.pdf


