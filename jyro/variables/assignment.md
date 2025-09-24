---
layout: default
title: Assignment
parent: Variables and Assignment
has_children: false
has_toc: false
permalink: /jyro/variables/assignment/
---

# Assignment

Assignment statements modify the value of existing variables or properties within objects and arrays. The assignment target can include property access and indexing operations to modify nested data structures.

```
Assignment       = AssignmentTarget "=" Expression ;
AssignmentTarget = Identifier { ( "." Identifier | "[" Expression "]" ) } ;
```

Assignment operations evaluate the right-hand expression completely before storing the result in the specified target location. Chained property access and array indexing allow modification of deeply nested data structures in a single statement.

**Valid Syntax:**
```jyro
counter = 5
user.name = "John"
items[0] = "first"
config["timeout"] = 30
nested.data[key] = value
```

**Invalid Syntax:**
```jyro
5 = counter            # Cannot assign to literal
user.name.length = 10  # Cannot assign to method result
```

**Important Considerations:**
- Assignment targets support property access and indexing
- Chained property/index access is permitted
- Assignment is not an expression and cannot be used within other expressions