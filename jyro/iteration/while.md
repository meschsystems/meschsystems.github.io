---
layout: default
title: Conditional Iteration (while, do, end)
parent: Iteration and Looping
has_children: false
has_toc: false
permalink: /jyro/iteration/while/
---

# Conditional Iteration (while, do, end)

While loops execute a statement block repeatedly as long as the specified condition evaluates to true. The condition is evaluated before each iteration, meaning the loop body may not execute at all if the condition is initially false.

```
WhileStmt        = "while" Expression "do" { Statement } "end" ;
```

The loop continues until the condition evaluates to false or until a `break` statement is encountered within the loop body. Care must be taken to ensure the condition will eventually become false to avoid infinite loops.

**Valid Syntax:**
```jyro
while counter < 10 do
    counter = counter + 1
    Process(counter)
end

while HasMoreData() do
    data = FetchNext()
    ProcessData(data)
end
```

**Invalid Syntax:**
```jyro
while counter < 10 {        # Missing 'do'
    counter = counter + 1
}

while counter < 10 do       # Missing 'end'
    counter = counter + 1
```

**Important Considerations:**
- `while` loops must be terminated with `end`
- The `do` keyword is required after the condition
- Infinite loops are possible if the condition never becomes false