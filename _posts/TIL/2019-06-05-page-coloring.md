---
layout: post
title: page coloring
categories: TIL
---

### Page(cache) Coloring 

Address translation allows pages of physical memory to be mapped into a process address space. 
Problem might accrue between cache and vm(virtual memory) since the virtual address 
on a process switch caches need to be flushed because they no longer contain the right data. 
physical address can break spatial locality if non-contiguous memory pages are mapped to contiguous ranges of virtual memory.
If virtually contiguous pages conflict int the cache.
 
### Solution
Use the Physical Addresses with smart allocation. 
Allocate pages that will show up in contiguous cache lines to contiguous addresses in the virtual memory. 