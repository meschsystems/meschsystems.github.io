---
layout: default
title: Standard Library Functions
parent: Function Calls
has_children: true
has_toc: false
permalink: /jyro/functions/stdlib
---

# Standard Library Functions

The Jyro standard library provides a comprehensive set of functions organized into logical categories for efficient data transformation and processing tasks.

## Mathematical Functions

Functions for numeric calculations and mathematical operations.

- [**Abs**](stdlib/math/abs/) - Calculate absolute value of a number
- [**Max**](stdlib/math/max/) - Find maximum value from multiple arguments
- [**Min**](stdlib/math/min/) - Find minimum value from multiple arguments
- [**RandomInt**](stdlib/math/randomint/) - Generate cryptographically secure random integer within range
- [**Round**](stdlib/math/round/) - Round number to specified decimal places
- [**Sum**](stdlib/math/sum/) - Calculate sum of multiple numeric arguments

## String Manipulation

Functions for processing and transforming text data.

- [**Contains**](stdlib/string/contains/) - Test if string contains substring or array contains value
- [**EndsWith**](stdlib/string/endswith/) - Test if string ends with specified suffix
- [**Join**](stdlib/string/join/) - Join array elements into single string with delimiter
- [**Lower**](stdlib/string/lower/) - Convert string to lowercase
- [**RandomString**](stdlib/string/randomstring/) - Generate cryptographically secure random string from character set
- [**Replace**](stdlib/string/replace/) - Replace all occurrences of substring with replacement
- [**Split**](stdlib/string/split/) - Split string into array using delimiter
- [**StartsWith**](stdlib/string/startswith/) - Test if string begins with specified prefix
- [**Trim**](stdlib/string/trim/) - Remove leading and trailing whitespace
- [**Upper**](stdlib/string/upper/) - Convert string to uppercase
- [**ToNumber**](stdlib/string/tonumber/) - Convert a string to a number

## Array Operations

Functions for manipulating and processing array data structures.

- [**Append**](stdlib/array/append/) - Add value to end of array
- [**Clear**](stdlib/array/clear/) - Remove all elements from array
- [**CountIf**](stdlib/array/countif/) - Count elements where field matches value using comparison operator
- [**Filter**](stdlib/array/filter/) - Return new array with elements matching field comparison criteria
- [**First**](stdlib/array/first/) - Return first element of array without modifying it
- [**GroupBy**](stdlib/array/groupby/) - Group array of objects by field value into keyed object
- [**IndexOf**](stdlib/array/indexof/) - Find index of element in array using deep equality
- [**Insert**](stdlib/array/insert/) - Insert value at specific array index
- [**Last**](stdlib/array/last/) - Return last element of array without modifying it
- [**MergeArrays**](stdlib/array/mergearrays/) - Combine multiple arrays into single array
- [**Pop**](stdlib/array/pop/) - Remove and return last array element
- [**RandomChoice**](stdlib/array/randomchoice/) - Select random element from array using cryptographically secure randomization
- [**RemoveAt**](stdlib/array/removeat/) - Remove element at specific index and return modified array
- [**RemoveLast**](stdlib/array/removelast/) - Remove last element and return modified array
- [**Reverse**](stdlib/array/reverse/) - Return new array with elements in reversed order
- [**Sort**](stdlib/array/sort/) - Return new sorted array using type-aware comparison
- [**SortByField**](stdlib/array/sortbyfield/) - Sort array of objects by specified field
- [**Take**](stdlib/array/take/) - Return new array containing first n elements without modifying original

## Date and Time Functions

Functions for handling date parsing, formatting, and calculations.

- [**DateAdd**](stdlib/dateandtime/dateadd/) - Add time interval to date
- [**DateDiff**](stdlib/dateandtime/datediff/) - Calculate difference between two dates
- [**DatePart**](stdlib/dateandtime/datepart/) - Extract specific component from date
- [**FormatDate**](stdlib/dateandtime/formatdate/) - Format date using specified pattern
- [**Now**](stdlib/dateandtime/now/) - Get current date and time in UTC
- [**ParseDate**](stdlib/dateandtime/parsedate/) - Parse date string into normalized format
- [**Today**](stdlib/dateandtime/today/) - Get current date without time components

## Utility Functions

Miscellaneous functions for inspecting and testing data types, value generation, and calling scripts.

- [**Base64Decode**](stdlib/utility/base64decode) - Decode Base64-encoded string back to original format
- [**Base64Encode**](stdlib/utility/base64encode) - Encode a string to Base64 format
- [**CallScript**](stdlib/utility/callscript/) - Execute Jyro script with isolated data context
- [**CallScript**](stdlib/utility/callscriptbyname/) - Execute named Jyro script via the host's script resolver with isolated data context
- [**Equal**](stdlib/utility/equal/) - Test equality between two values
- [**Exists**](stdlib/utility/exists/) - Test if value is not null
- [**InvokeRestMethod**](stdlib/utility/invokerestmethod/) - Execute HTTP REST API requests (experimental)
- [**IsNull**](stdlib/utility/isnull/) - Test if value is null
- [**Keys**](stdlib/utility/keys/) - Get array of property names from an object
- [**Length**](stdlib/utility/length/) - Get length/count of strings, arrays, or objects
- [**NewGuid**](stdlib/utility/newguid) - Generate a new globally unique identifier (GUID)
- [**NotEqual**](stdlib/utility/notequal/) - Test inequality between two values
- [**TypeOf**](stdlib/utility/typeof/) - Get type name of value as string

## Usage Patterns

Most functions follow consistent patterns for parameter handling and return values:

- **Immutable Transformations**: Functions like `Sort`, `Reverse`, and `Filter` return new arrays without modifying the original, enabling predictable data flow and safe composition
- **Chainable Operations**: Array-returning functions can be composed together (e.g., `Filter(Sort(Filter(...)))`) for powerful data transformations
- **Type Coercion**: Functions automatically handle reasonable type conversions (e.g., converting values to strings in `Join`)
- **Error Handling**: Functions return null or default values for invalid inputs rather than throwing exceptions
- **Safe Access**: Functions like `First`, `Last`, and `Pop` return null for empty arrays instead of throwing errors
- **Consistent Operators**: Functions like `Filter` and `CountIf` support comparison operators: `"=="`, `"!="`, `"<"`, `"<="`, `">"`, `">="`