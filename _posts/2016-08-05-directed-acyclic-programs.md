---
layout: post
title:  "Programs as DAGs"
date:   2016-08-05
---

### Programs Should Be Directed Acyclic Graphs

One of the biggest problems in software world is that most of the people don’t really care about what would happen when their program gets bigger.

<div class="figure">
    <img src="/images/directed-acyclic-graph.png"/>
</div>

It is very dangerous to write code that has potential to change something vital in the program. (aka **Side Effects!**)
Let’s think about the code as a graph and make some assumptions so that;
- An expression is a node in the graph.
- Edges (connections between nodes) are the calls to other expressions inside expressions (parameters of functions).
- `e1(e2, e3)` means `e1` is connected to `e2` and `e3`.

To be continued…