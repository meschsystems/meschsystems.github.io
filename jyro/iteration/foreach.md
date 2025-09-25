---
layout: default
title: Collection Iteration (foreach, in, do, end)
parent: Iteration and Looping
has_children: false
has_toc: false
permalink: /jyro/iteration/foreach/
---

# Collection Iteration (foreach, in, do, end)

The `foreach` statement executes a statement block for each element in a collection, automatically handling iteration over arrays and objects. An iterator variable is automatically declared and assigned each element value during iteration.

```
ForEachStmt      = "foreach" Identifier "in" Expression "do"
                     { Statement }
                   "end" ;
```

For arrays, the iterator variable receives each element value in order. For objects, the iterator variable receives each property value. The iterator variable is automatically scoped to the loop and shadows any existing variable with the same name.

**Valid Syntax:**
```jyro
foreach item in Data.items do
    ProcessItem(item)
end

foreach user in userList do
    ValidateUser(user)
    SaveUser(user)
end

foreach item in array ["car", "box", "table", "dog"] do   # Note use of array to declare an array literal
    ProcessItem(item)
end
```

**Notes**
- The iterator variable is automatically declared and scoped to the loop
- Use `in` keyword, not `of` or other variants
- The expression must evaluate to an iterable collection
- Iterator variable shadows any existing variable with the same name