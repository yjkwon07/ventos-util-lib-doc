---
title: allEqual
sidebar_position: 1
---

# allEqual

The `allEqual` function is a utility function that checks if all elements in an array are equal. It is generic, meaning it can handle arrays of any type.

## Function Signature

```ts
const allEqual = <T>(arr: T[]) => boolean;
```

## Parameters

`arr: T[]`: An array of type `T`, where `T` can be any type (e.g., number, string, boolean, etc.).

## Returns

`boolean`: The function returns `true` if all elements in the array are equal, and `false` otherwise. If the array is empty, it returns `false`.

## Examples

### Example 1: Array of Numbers

```ts
const result = allEqual([1, 1, 1, 1]); 
console.log(result); // Output: true
```

### Example 2: Array of Strings

```ts
const result = allEqual(['a', 'a', 'a']); 
console.log(result); // Output: true
```

### Example 3: Array with Mixed Values
```ts
const result = allEqual([1, 2, 3, 1]); 
console.log(result); // Output: false
```

### Example 4: Empty Array
```ts
const result = allEqual([]); 
console.log(result); // Output: false
```

## How It Works

1. The function first checks if the array is empty using `arr.length === 0`. If it is, the function returns `false`.

2. If the array is not empty, it uses the `every` method to check if every element in the array is strictly equal (`===`) to the first element `arr[0]`.

3. If all elements match, it returns `true`. If any element is different, it returns `false`.