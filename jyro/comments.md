---
layout: default
title: Comments
parent: Jyro Language Syntax
has_children: false
has_toc: false
permalink: /jyro/comments/
---

# Comments

Comments begin with `#` and continue to the end of the line. Comments may be placed on their own line or at the end of a statement. Multi-line comments are written with a `#` at the beginning of each line. Comments are typically stripped out of a Jyro script when it is compiled and have no effect on execution.

**Valid Syntax:**
```jyro
# This is a single-line comment
var counter = 0

# This is a
# multi-line comment
ProcessData()

# Comments can be split...
DoFoo()  #... with statements in between
```