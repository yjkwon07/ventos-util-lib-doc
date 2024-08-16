---
title: calculatePrefixSum
sidebar_position: 3
---

# calculatePrefixSum

The `calculatePrefixSum` function calculates the sum of a subarray within a given list of numbers up to a specified index. This is useful for operations where you need the cumulative sum up to a certain point in the array.

## Function Signature

```ts
const calculatePrefixSum = (lengthList: number[], index: number) => number;
```

## Parameters

`lengthList: number[]`: An array of numbers. The function will calculate the sum of the elements up to the specified index.

`index: number`: The index up to which the sum should be calculated. This index is inclusive.

## Returns

`number`: The sum of the elements in the array from the start up to the specified index.

## Example Usage

### Example 1: Basic Usage

```typescript
const lengthList = [3, 4, 2];
const index = 1;
const result = calculatePrefixSum(lengthList, index);
console.log(result); // 출력: 7
```

This example takes the sum of the first two elements of the array [3, 4], resulting in 7.

## Explanation

1. `Array Slicing`: The function uses `slice(0, index + 1)` to create a subarray that includes elements from the start of the array up to and including the specified index.

2. `Cumulative Sum`: The `reduce` method is then used to sum the values in the sliced array. The initial value of the accumulator (`acc`) is set to 0.

3. `Return Value:` The function returns the total sum of the specified subarray.