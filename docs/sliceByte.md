---
title: sliceByte
sidebar_position: 11
---

# sliceByte

The `sliceByte` function truncates a string to a specified byte length. It handles ASCII characters, multi-byte characters, and special symbols correctly, ensuring that the output remains valid UTF-8.

## Function Signature

```ts
const sliceByte = (text: string, len: number) => string;
```

## Parameters

`text`: string: The input string to be truncated.

`len`: number: The maximum byte length of the truncated string.

## Returns

`string`: A substring of the original text truncated to fit within the specified byte length.

## Example Usage

### Example 1: Slicing ASCII Characters Correctly

```typescript
const result = sliceByte('hello world', 5);
console.log(result);
// Output: 'hello'
```

### Example 2: Slicing Mixed ASCII and Non-ASCII Characters Correctly

```typescript
const result = sliceByte('hello世界', 8);
console.log(result);
// Output: 'hello世' // 'hello' (5 bytes) + '世' (3 bytes)
```

### Example 3: Slicing Non-ASCII Characters Correctly

```typescript
const result1 = sliceByte('世界', 3);
console.log(result1);
// Output: '世' // '世' (3 bytes)

const result2 = sliceByte('世界', 6);
console.log(result2);
// Output: '' // '世界' (6 bytes)
```

### Example 4: Handling Special Characters Correctly

```typescript
const result = sliceByte('hello!@#', 8);
console.log(result);
// Output: '' // 'hello!@#' (8 bytes, so the function returns an empty string as the length exceeds)
```

### Example 5: Handling Empty String

```typescript
const result = sliceByte('', 5);
console.log(result);
// Output: ''
```

### Example 6: Handling Numeric Characters

```typescript
const result = sliceByte('1234567890', 5);
console.log(result);
// Output: '12345'
```

### Example 7: Handling Multi-Byte Characters Including Emojis

```typescript
const result1 = sliceByte('hello😀world', 11);
console.log(result1);
// Output: 'hello😀wo' // 'hello' (5 bytes) + '😀' (4 bytes) + 'wo' (2 bytes)

const result2 = sliceByte('😀😀😀', 8);
console.log(result2);
// Output: '😀😀' // '😀' (4 bytes) + '😀' (4 bytes)
```

### Example 8: Handling Mixed Content

```typescript
const result = sliceByte('hello 123 世界!', 10);
console.log(result);
// Output: 'hello 123 ' // 'hello 123' (9 bytes) + ' ' (1 byte)
```

### Example 9: Handling Accented Characters

```typescript
const result = sliceByte('café', 5);
console.log(result);
// Output: '' // 'c' (1 byte) + 'a' (1 byte) + 'f' (1 byte) + 'é' (2 bytes) = 5 bytes
```

### Example 10: Handling Newline and Tab Characters

```typescript
const result = sliceByte('hello\nworld\t!', 6);
console.log(result);
// Output: 'hello\n'
```

## Explanation

1. `Encoding and Decoding`: The function uses `TextEncoder` to encode the string into bytes and `TextDecoder` to decode it back into a string.

2. `Byte Truncation`: It iterates over the encoded bytes, checking the length to ensure it doesn't exceed the specified byte limit, and then slices the byte array accordingly.

3. `Handling Multi-Byte Characters`: The function properly handles multi-byte characters and ensures that the output string is valid UTF-8.