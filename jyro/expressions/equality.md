---
layout: default
title: Equality (==, !=)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/equality/
---

# Equality (==, !=)

Equality operators compare values for equivalence or difference. The comparison behavior depends on the types of the operands and follows the runtime's equality semantics.

```
Equality         = Relational { ("==" | "!=") Relational } ;
```

**Examples:**
```jyro
name == "admin"
status != "pending"
```

<a name="relational-operators"></a>