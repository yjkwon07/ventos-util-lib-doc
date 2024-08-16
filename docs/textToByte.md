---
title: textToByte
sidebar_position: 12
---

# textToByte

The `textToByte` function calculates the byte size of a given string when encoded in UTF-8. It uses the `TextEncoder` API to convert the string into bytes and returns the length of the encoded byte array.

## Function Signature

```ts
const textToByte = (text: string) => number;
```

## Parameters

`text`: string: The input string whose byte size needs to be calculated.

## Returns

`number`: The byte size of the input string in UTF-8 encoding.

## Example Usage

### Example 1: Calculating Byte Size for ASCII Characters

```typescript
const byteSize = textToByte('hello');
console.log(byteSize);
// Output: 5
```

### Example 2: Calculating Byte Size for Mixed ASCII and Non-ASCII Characters

```typescript
const byteSize = textToByte('hello世界');
console.log(byteSize);
// Output: 11 // 'hello' (5 bytes) + '世界' (6 bytes, 3 bytes each)
```

### Example 3: Calculating Byte Size for Non-ASCII Characters

```typescript
const byteSize = textToByte('世界');
console.log(byteSize);
// Output: 6 // '世界' (6 bytes, 3 bytes each)
```

### Example 4: Calculating Byte Size for Special Characters

```typescript
const byteSize = textToByte('!@#');
console.log(byteSize);
// Output: 3
```

### Example 5: Calculating Byte Size for Empty String

```typescript
const byteSize = textToByte('');
console.log(byteSize);
// Output: 0
```

### Example 6: Calculating Byte Size for Numeric Characters

```typescript
const byteSize = textToByte('12345');
console.log(byteSize);
// Output: 5
```

### Example 7: Calculating Byte Size for Multi-Byte Characters Including Emojis

```typescript
const byteSize1 = textToByte('😀');
console.log(byteSize1);
// Output: 4 // Emoji '😀' is 4 bytes

const byteSize2 = textToByte('hello😀world');
console.log(byteSize2);
// Output: 11 // 'hello' (5 bytes) + '😀' (4 bytes) + 'world' (6 bytes)
```

### Example 8: Calculating Byte Size for Mixed Content

```typescript
const byteSize = textToByte('hello 123 世界!');
console.log(byteSize);
// Output: 17 // 'hello' (5 bytes) + ' ' (1 byte) + '123' (3 bytes) + ' ' (1 byte) + '世界' (6 bytes) + '!' (1 byte)
```

### Example 9: Calculating Byte Size for Accented Characters

```typescript
const byteSize = textToByte('café');
console.log(byteSize);
// Output: 5 // 'c' (1 byte) + 'a' (1 byte) + 'f' (1 byte) + 'é' (2 bytes)
```

### Example 10: Calculating Byte Size for Newline and Tab Characters

```typescript
const byteSize = textToByte('\n\t');
console.log(byteSize);
// Output: 2 // '\n' (1 byte) + '\t' (1 byte)
```

## Explanation

1. `Encoding`: The function uses TextEncoder to convert the string to a UTF-8 encoded byte array.

2. `Byte Calculation`: The length of the byte array is determined using the `length` property, which provides the byte size of the string in UTF-8 encoding.

3. `Multi-Byte Characters`: Properly handles multi-byte characters, including non-ASCII characters and emojis, to accurately reflect their byte size.