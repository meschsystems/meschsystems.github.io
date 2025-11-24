---
layout: default
title: RandomChoice
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/randomchoice/
---

# RandomChoice

Selects a random element from an array using cryptographically secure randomization.

## Syntax

```jyro
RandomChoice(array)
```

## Parameters

- **array** (array): The array to select a random element from. Must not be empty.

## Returns

- **any**: A randomly selected element from the array

## Description

Returns a random element from the provided array using cryptographically secure randomization. Each element has an equal probability of being selected.

Uses `System.Security.Cryptography.RandomNumberGenerator` for cryptographic security rather than pseudo-random generation, ensuring unpredictable selection suitable for security contexts.

Throws an error if the array is empty, as there are no elements to select from.

## Examples

```jyro
# Select random fruit
var fruits = ["apple", "banana", "orange", "grape"]
var random_fruit = RandomChoice(fruits)
# random_fruit could be any of the fruits
```

```jyro
# Select random number
var numbers = [1, 2, 3, 4, 5]
var random_num = RandomChoice(numbers)
# random_num could be 1, 2, 3, 4, or 5
```

```jyro
# Select random configuration
var configs = [
    { "server": "prod-1", "region": "us-east" },
    { "server": "prod-2", "region": "us-west" },
    { "server": "prod-3", "region": "eu-central" }
]

var selected_config = RandomChoice(configs)
# selected_config is one of the configuration objects
```

```jyro
# Random greeting
var greetings = ["Hello", "Hi", "Hey", "Greetings"]
var greeting = RandomChoice(greetings)
Data.message = greeting + ", " + Data.username
```

```jyro
# Random color selection
var colors = ["red", "blue", "green", "yellow", "purple"]
var color = RandomChoice(colors)
Data.theme_color = color
```

```jyro
# Select random winner from participants
var participants = ["Alice", "Bob", "Carol", "Dave", "Eve"]
var winner = RandomChoice(participants)
# winner is randomly selected from participants
```

```jyro
# Random load balancing
var servers = ["server1.example.com", "server2.example.com", "server3.example.com"]
var target_server = RandomChoice(servers)
# Randomly distributes load across servers
```

```jyro
# Select random test case
var test_cases = GetAllTestCases()
var random_test = RandomChoice(test_cases)
ExecuteTest(random_test)
# Runs a randomly selected test
```

```jyro
# Random sampling pattern
var population = GetAllUsers()
var sample = []
var i = 0
while i < 10 do
    var random_user = RandomChoice(population)
    sample = Append(sample, random_user)
    i = i + 1
end
# Creates a random sample of 10 users
```

```jyro
# Single element array always returns that element
var single = ["only"]
var choice = RandomChoice(single)
# choice is always "only"
```

## Notes

- Uses cryptographically secure random selection (not pseudo-random)
- Each element has equal probability of being selected
- Throws an error if the array is empty (cannot select from nothing)
- Works with arrays containing any type of elements (numbers, strings, objects, nested arrays)
- Does not modify the original array
- For random integer generation, see [RandomInt](../math/randomint/)
- For random string generation, see [RandomString](../string/randomstring/)
- Each call produces an independent random selection (no seeding required)
- For random sampling without replacement, combine with array manipulation functions
