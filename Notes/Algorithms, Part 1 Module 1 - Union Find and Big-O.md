---
tags:
  - module
lecture_count: "5"
current_lecture: "1"
length: 
status: Ongoing
course_link: "[[Algorithms, Part 1]]"
link: https://www.coursera.org/learn/algorithms-part1/supplement/aYr6R/overview
module_number: 1
lecture_slides: "[[Algs4-Lecture1-UnionFind.pdf]]"
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] Apply the union-find data type to solve problems in science, engineering, and industry.
- [ ] Define the union-find (or disjoint sets) data type.
- [ ] Compare the performance of different algorithms for the union-find data type.
- [ ] Design different algorithms (quick find, quick union, weighted quick union, path compression) for the union-find data type.
- [ ] Develop Java implementations of different algorithms for the union-find data type.
- [ ] Use the parent-link representation to represent tree data structures.

```

We illustrate our basic approach to developing and analyzing algorithms by considering the dynamic connectivity problem. We introduce the union−find data type and consider several implementations (quick find, quick union, weighted quick union, and weighted quick union with path compression). Finally, we apply the union−find data type to the percolation problem from physical chemistry.

**Suggested Readings:** Section 1.4 and 1.5

## Lecture 1: Dynamic Connectivity
---

The first step to develop a useful algorithm is to *model* the problem. Try to understand what are the main elements of the problem that need to be solved. Then we'll find some *algorithm* to solve the problem. If that doesn't work, what we do is try to figure out why, find a way to address whatever's causing that problem, find a new algorithm and *iterate* until we're satisfied.

This is the scientific approach to designing and analyzing algorithms, where we build mathematical models to try and understand what's going on, and then we do experiments to validate those models and help us improve things. 

So, first we'll talk about the dynamic connectivity problem, the model of the problem for **union find**.

#### Modeling the connections
---

We assume that "is connected to" is equivalent to:
- **Reflexive:** <i>p</i> is connected to *p*
- **Symmetric:** If *p* is connected to *n*, then *n* is connected to *p* 
- **Transitive:** If *p* is connected to *n* and *n* is connected to *d*, then *p* is connected to *d*.


**Connected Components** are the *set* of objects that are mutually connected. They have the property that if any two objects in them are connected and there is no object outside that is connected to those objects, that's connected components. Each number representing an object.

![[Pasted image 20240429144257.png | center]]


#### Implementing the operations
---

To implement the operations, we have the **find query** and the **union command**. And so we're going to maintain the connected components. 

- **Find**: Check if two objects are in the same component
- **Union**: Replace components containing two objects with their union.

![[Pasted image 20240429145631.png | center]]

All of that leads up to, in a programming world, to specifying a data type which is simply specification of the methods that we are want to going to implement in order to solve this problem. IE Create a class.


#### Union-find data type (API)
---

**Goal:** Design an efficient data structure for union-find.
- **N** objects (0 to N - 1)
- **M** operations
- Find queries and union commands may be intermixed.

![[algs4-UF-model.png | center]]



#### Dynamic Connectivity Problem Solution 1: Quick-find (eager approach)
---

- Integer array `id[]` of size **N**
- Interpretation: **p** and **q** objects are connected *if* they have the same id.

![[Pasted image 20240430095026.png | center]]


That's going to support a quick implementation of the `find()` operation. Union is more difficult; in order to merge the components, containing two given objects, we have to change all the entries whose ID is equal to one of them to the other one.

- **Find** Check if **p** and **q** have the same id.
- **Union** To merge components containing **p** and **q**, change all entries whose id equals `id[p]` to `id[q]`
	- Before
	  ![[Pasted image 20240430095721.png | center]]
	- After
	  ![[Pasted image 20240430095809.png | center]]


``````ad-example
title: Quick-find Demo

```java
public class QuickFindUF {
    private int[] id;

    public QuickFindUF(int N) {
        id = new int[N]; // N array accesses

        for (int i = 0; i < N; i++)
            id[i] = i;
    }

    public boolean connected(int p, int q) {
        return id[p] == id[q]; // 2 array accesses
    }

    public void union(int p, int q) {
        int pid = id[p];
        int qid = id[q];

        // Change all entries with id[p] to id[q] (2N + 2)
        for (int i = 0; i < id.length; i++)
            if (id[i] == pid) id[i] = qid;
    }
}
```


``````


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
