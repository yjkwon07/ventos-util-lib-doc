---
title: divideIntoChunkList
sidebar_position: 5
---

# divideIntoChunkList

The `divideIntoChunkList` function splits an array into smaller chunks of a specified size. It handles cases where the array length is not perfectly divisible by the chunk size and returns the remaining elements in the final chunk.

## Function Signature

```typescript
const divideIntoChunkList = <E>(arr: E[], size: number) => E[][];
```

## Parameters

`arr: E[]`: The array to be divided into chunks.

`size`: number: The size of each chunk. Must be greater than 0.

## Returns

`E[][]`: A two-dimensional array where each inner array is a chunk of the specified size.

## Example Usage

### Example 1: Divide Array into Chunks
```typescript
const arr = [1, 2, 3, 4, 5];
const size = 2;
const result = divideIntoChunkList(arr, size);
console.log(result); // Output: [[1, 2], [3, 4], [5]]
```

### Example 2: Handle Array Length Not Perfectly Divisible by Size

```typescript
const arr = [1, 2, 3, 4, 5, 6, 7];
const size = 3;
const result = divideIntoChunkList(arr, size);
console.log(result); // Output: [[1, 2, 3], [4, 5, 6], [7]]
```

### Example 3: Handle Empty Array

```typescript
const arr: any[] = [];
const size = 3;
const result = divideIntoChunkList(arr, size);
console.log(result); // Output: []
```

### Example 4: Handle Size Larger Than Array Length

```typescript
const arr = [1, 2, 3];
const size = 5;
const result = divideIntoChunkList(arr, size);
console.log(result); // Output: [[1, 2, 3]]
```

### Example 5: Handle Size of 1

```typescript
const arr = [1, 2, 3, 4];
const size = 1;
const result = divideIntoChunkList(arr, size);
console.log(result); // Output: [[1], [2], [3], [4]]
```

### Example 6: Handle Size of 0 or Negative

```typescript
const arr = [1, 2, 3, 4];

try {
  divideIntoChunkList(arr, 0);
} catch (e) {
  console.log(e.message); // Output: 'Invalid input: size should set 0 over'
}

try {
  divideIntoChunkList(arr, -2);
} catch (e) {
  console.log(e.message); // Output: 'Invalid input: size should set 0 over'
}
```

## Explanation

1. `Input Validation`: The function checks if the size is less than or equal to 0. If so, it throws an error with a message: 'Invalid input: size should set 0 over'.

2. `Chunk Creation`: The function uses a while loop to slice the array into chunks of the specified size. It continues until all elements of the array have been processed.

3. `Return Value`: The function returns a two-dimensional array where each inner array represents a chunk of the original array.