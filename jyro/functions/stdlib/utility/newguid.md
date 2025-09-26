---
layout: default
title: NewGuid
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/newguid/
---

# NewGuid

Generates a new globally unique identifier (GUID) and returns it as a string.

## Syntax

```jyro
NewGuid()
```

## Parameters

None

## Returns

- **string**: A newly generated GUID in standard format (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)

## Description

Creates a new random GUID each time it is called, providing a unique identifier suitable for tracking, correlation, or identification purposes. The generated GUID follows the standard format and uses the system's cryptographically secure random number generator, ensuring uniqueness across different machines and time periods.

## Examples

```jyro
var id1 = NewGuid()    # Returns something like "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
```

```jyro
var id2 = NewGuid()    # Returns a different GUID each time
```

```jyro
# Creating unique identifiers for records
Data.recordId = NewGuid()
Data.sessionId = NewGuid()
```

```jyro
# Using in loops to generate multiple unique IDs
foreach item in Data.items do
    item.uniqueId = NewGuid()
end
```