---
title: commaFormat
sidebar_position: 4
---

# commaFormat

The `commaFormat` function formats a given number or string by inserting commas at regular intervals for better readability. By default, commas are inserted every three digits.

## Function Signature

```ts
const commaFormat = (inputNumber: number | string, count: number = 3) => string;
```

## Parameters

`inputNumber: number | string`: The number or string to be formatted.

`count: number` (optional): The number of digits between each comma. Defaults to 3.

## Returns

`string`: A string representation of the number with commas inserted at the specified intervals.

## Example Usage

### Example 1: Default Formatting (Every 3 Digits)

```typescript
console.log(commaFormat(1000)); // Output: '1,000'
console.log(commaFormat(1000000)); // Output: '1,000,000'
console.log(commaFormat(1234567890)); // Output: '1,234,567,890'
```

### Example 2: Formatting String Representations of Numbers

```typescript
console.log(commaFormat('1000')); // Output: '1,000'
console.log(commaFormat('1000000')); // Output: '1,000,000'
console.log(commaFormat('1234567890')); // Output: '1,234,567,890'
```

### Example 3: Handling Decimal Numbers

```typescript
console.log(commaFormat(1234.56)); // Output: '1,234.56'
console.log(commaFormat('1234.56')); // Output: '1,234.56'
```

### Example 4: Handling Numbers with Leading Zeros

```typescript
console.log(commaFormat('0001234')); // Output: '0,001,234'
```

### Example 5: Handling Falsy Inputs

```typescript
console.log(commaFormat(0)); // Output: '0'
console.log(commaFormat('')); // Output: '0'
```

### Example 6: Formatting Negative Numbers

```typescript
console.log(commaFormat(-1000)); // Output: '-1,000'
console.log(commaFormat('-1000000')); // Output: '-1,000,000'
```

### Example 7: Custom Formatting (Every 2 Digits)

```typescript
console.log(commaFormat(123456, 2)); // Output: '12,34,56'
console.log(commaFormat('12345678', 2)); // Output: '12,34,56,78'
```

### Example 8: Custom Formatting (Every 4 Digits)

```typescript
console.log(commaFormat(1234567890, 4)); // Output: '12,3456,7890'
console.log(commaFormat('12345678901234', 4)); // Output: '12,3456,7890,1234'
```

## Explanation

1. `Regex for Comma Insertion`: The function uses a regular expression to insert commas. The `RegExp` is dynamically created based on the `count` parameter, which determines how many digits should appear between commas.

2. `Input Type Handling`: The function first converts the `inputNumber` to a string, ensuring that both numeric and string inputs are treated consistently.

3. `Falsy Input`: If the inputNumber is falsy (like `0` or an empty string), the function returns '`0`'.

4. `Negative Numbers`: The function handles negative numbers correctly by placing the comma after the negative sign.