---
layout: default
title: Idiomatic Patterns
parent: Jyro Language Reference
has_children: false
has_toc: true
permalink: /jyro/idiomatic-patterns/
nav_order: 140
---

# Idiomatic Patterns

Common patterns for solving typical Jyro tasks.

## Input validation with guard clauses

Validate inputs early and exit on failure:

```jyro
if Data.items is null or Data.items is not array then
    fail "Items must be an array"
end

if Length(Data.items) == 0 then
    Data.result = []
    return "No items to process"
end

if Data.email is null or Data.email == "" then
    fail "Email is required"
end

# Proceed with valid data
```

## Safe property access

Use short-circuit evaluation to prevent null reference errors:

```jyro
if Data.user is not null and Data.user.profile is not null then
    Data.userName = Data.user.profile.name
else
    Data.userName = "Guest"
end

# Null coalescing for simple defaults
var name = Data.user.name ?? "Unknown"
```

## Array processing pipeline

Chain query and array functions to build a filter-sort-extract pipeline:

```jyro
var active = WhereByField(Data.employees, "active", "==", true)
var engineering = WhereByField(active, "department", "==", "Engineering")
var sorted = SortByField(engineering, "salary", "desc")
var names = Select(sorted, "name")
Data.topEngineers = names
```

## Aggregation with select

Extract field values first, then aggregate:

```jyro
var prices = Select(Data.items, "price")
Data.total = Sum(prices)
Data.average = Average(prices)
Data.highest = Max(prices)
Data.lowest = Min(prices)
```

## Configuration defaults with merge

Use `Merge` to apply user overrides on top of defaults:

```jyro
Data.config = Merge([
    {"timeout": 30, "retries": 3, "debug": false},   # Defaults
    Data.config                                        # User overrides
])
```

## Data enrichment

Add computed properties to the `Data` context:

```jyro
Data.count = Length(Data.items)
Data.total = Sum(Select(Data.items, "price"))
Data.hasItems = Length(Data.items) > 0
Data.uniqueCategories = Distinct(Select(Data.items, "category"))
return
```

## Chained transforms

Pipe results through a sequence of functions:

```jyro
var names = Select(Data.users, "name")
var upper = Map(names, n => ToUpper(n))
var sorted = Sort(upper)
Data.result = Join(sorted, ", ")
```

## Accumulation with loops

When lambdas and query functions are insufficient for complex per-item logic, use a manual loop:

```jyro
var total = 0
foreach item in Data.items do
    if item.price is number and item.taxable then
        total += item.price * 1.1
    elseif item.price is number then
        total += item.price
    end
end
Data.totalWithTax = total
```

## Collecting nested arrays

Flatten nested array fields and deduplicate:

```jyro
var allTags = SelectMany(Data.documents, "tags")
Data.uniqueTags = Distinct(allTags)
```

## API response shaping

Use `Project` and `Omit` to control which fields appear in output:

```jyro
var activeUsers = WhereByField(Data.users, "active", "==", true)
Data.response = Project(activeUsers, ["id", "name", "email"])
Data.sanitized = Omit(Data.users, ["password", "token", "secret"])
```

## "Private" members for metadata

Start identifier names with an underscore to differentiate metadata or data returned for further host processing from business data:

```jyro
Data._debug = {...}
Data._processingStats = {...}
Data._payload = {...}
```
