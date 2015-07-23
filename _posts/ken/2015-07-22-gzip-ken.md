---
layout: post
category : java
tagline: "Supporting tagline"
tags : [java]
---
{% include JB/setup %}


# java gzip压缩问题
1. 在使用gzip时候,由于没有调用GZIPOutputStream和GZIPInputStream的close()方法,导致分配的java堆内存没有释放的问题.这个是由于自己的疏忽导致的.该BS.
