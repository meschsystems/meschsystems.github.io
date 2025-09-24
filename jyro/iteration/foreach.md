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

**Invalid Syntax:**
```jyro
foreach item of items do    # Must use 'in', not 'of'
    ProcessItem(item)
end

foreach items do            # Missing iterator variable and 'in'
    ProcessItem()
end
```

The `Expression` after `in` can be any valid expression, and `ArrayLiteral` is part of the `Primary` expressions. So yes, this should be syntactically valid:

The grammar supports any expression that evaluates to an iterable collection, so you these are also valid syntax:

```jyro
foreach activeUser in GetActiveUsers() do      # Assuming host-side function GetActiveUsers() returns an array

foreach entry in (condition and arrayA or arrayB) do       # All conditions must result in an array
```

**Important Considerations:**
- The iterator variable is automatically declared and scoped to the loop
- Use `in` keyword, not `of` or other variants
- The expression must evaluate to an iterable collection
- Iterator variable shadows any existing variable with the same name