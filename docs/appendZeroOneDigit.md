---
title: appendZeroOneDigit
sidebar_position: 2
---

# appendZeroOneDigit

The `appendZeroOneDigit` function adds a leading zero to a single-digit number, converting it to a string. It handles both string and number inputs, ensuring the output is always a string.

## Function Signature

```ts
const appendZeroOneDigit = (num: string | number) => string;
```

## Parameters

`num: string | number`: The input value, which can be either a `number` or a `string` that represents a number.

## Returns

`string`:

  - If the number is a single-digit (0-9), the function returns a string with a leading zero (e.g., 07).

  - If the number is greater than or equal to 10, or negative, it returns the number as a string without modification.

## Example Usage

### Example 1: Single-digit number

```ts
const result = appendZeroOneDigit(7); console.log(result); // 출력: '07'
```

### Example 2: Double-digit number

```ts
const result = appendZeroOneDigit(12); console.log(result); // 출력: '12'
```

### Example 3: String input with single-digit

```ts
const result = appendZeroOneDigit('3'); console.log(result); // 출력: '03'
```

### Example 4: String input with double-digit

```ts
const result = appendZeroOneDigit('15'); console.log(result); // 출력: '15'
```

### Example 5: Invalid input

```ts
try { appendZeroOneDigit('abc'); } catch (e) { console.log(e.message); } // 출력: 'Invalid input: input should be a number or a string that can be converted to a number'
```

## Explanation

1. `Input Type Check`: The function first checks if the input is a string. If so, it converts the string to an integer using `parseInt`.

2. `NaN Check:` If the input cannot be converted to a valid number, an error is thrown with a descriptive message.

3. `Single-Digit Check`: If the number is between 0 and 9 (inclusive), the function adds a leading zero and returns it as a string.

4. `Other Cases`: For all other valid numbers, the function simply returns the number as a string