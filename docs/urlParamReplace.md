---
title: urlParamReplace
sidebar_position: 15
---

# urlParamReplace

The `urlParamReplace` function substitutes placeholders in a URL with actual values. Placeholders in the URL are denoted by `:key` syntax, where `key` corresponds to a key in the `param` object.

## Function Signature

```typescript
const urlParamReplace = (url: string, param: { [key: string]: any }) => string;
```

## Parameters

`url: string`: The URL template containing placeholders.

`param: { [key: string]: any }`: An object where keys are placeholder names and values are the replacements for those placeholders.

## Returns

`string`: The URL with placeholders replaced by the corresponding values from the param object.

## Example Usage

### Basic Replacement

```typescript
const url = '/user/:id';
const param = { id: 123 };
const result = urlParamReplace(url, param);
console.log(result);
// Output: '/user/123'
```

### Multiple Replacements

```typescript
const url = '/user/:id/profile/:profileId';
const param = { id: 123, profileId: 456 };
const result = urlParamReplace(url, param);
console.log(result);
// Output: '/user/123/profile/456'
```

### Handling Different Parameter Types

```typescript
const url = '/user/:isActive';
const param = { isActive: true };
const result = urlParamReplace(url, param);
console.log(result);
// Output: '/user/true'
```