---
layout: post
title:  "Writing Cache-friendly Ruby"
date:   2017-04-02 15:54:34 -0500
published: true
---

While learning about how hardware caching is implemented in a computer architecture class, for fun, I ran some benchmarks on C code accessing a 2D array in row-major vs. column-major. The row-major code ran in `0.000001` seconds, whereas the column-major code ran in `0.224663` seconds. This is due to the way caching memory is laid out in the cache.

It occured to me afterwards to test if Ruby had a similiar issue. After running the same test in C, Ruby row-major code ran in `1.471860` seconds, whereas the column-major code ran in `1.609366` seconds. So, if you want a quick speed fix when dealing with multi-dimensional arrays, flip those i's and j's. 