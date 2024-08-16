---
title: flatten
sidebar_position: 6
---

# flatten

The `flatten` function transforms a nested list of objects into a flat list while preserving parent-child relationships. It can add a reference to the parent object in each child object if specified.

## Function Signature

```ts
const flatten = <T extends Record<string, any>>(
  dataList: T[],
  {
    childrenKeyName,
    parentCreateKeyName,
    idKeyName,
    parentValue,
  }: {
    childrenKeyName: KeysOfUnion<T>;
    parentCreateKeyName?: string;
    idKeyName?: KeysOfUnion<T>;
    parentValue?: string;
  },
): T[];
```

## Parameters

`dataList: T[]`: The list of nested objects to be flattened.

`childrenKeyName: KeysOfUnion<T>`: The key name that holds child elements within each object.

`parentCreateKeyName?: string`: (Optional) The key name to add in child objects to reference their parent.

`idKeyName?: KeysOfUnion<T>`: (Optional) The key name used to find the parent's ID.

`parentValue?: string`: (Optional) The value to set for `parentCreateKeyName` in the top-level object.

## Returns

`T[]`: A flattened list of objects, each including a reference to its parent if specified.

## Example Usage

### Example 1: Flatten Nested Objects

```typescript
const dataList = [
  {
    id: 1,
    name: 'Parent',
    children: [
      { id: 2, name: 'Child 1' },
      { id: 3, name: 'Child 2', children: [{ id: 4, name: 'Grandchild' }] },
    ],
  },
];

const result = flatten(dataList, {
  childrenKeyName: 'children',
  parentCreateKeyName: 'parentId',
  idKeyName: 'id',
  parentValue: '',
});
console.log(result);
// Output: [
//   { id: 1, name: 'Parent', parentId: '', children: [...] },
//   { id: 2, name: 'Child 1', parentId: 1 },
//   { id: 3, name: 'Child 2', parentId: 1, children: [...] },
//   { id: 4, name: 'Grandchild', parentId: 3 },
// ]
```

### Example 2: Add Parent Reference Key

```typescript
const dataList = [
  {
    id: 1,
    name: 'Parent',
    children: [{ id: 2, name: 'Child 1' }],
  },
];

const result = flatten(dataList, {
  childrenKeyName: 'children',
  parentCreateKeyName: 'parentId',
  idKeyName: 'id',
  parentValue: '',
});
console.log(result);
// Output: [
//   { id: 1, name: 'Parent', parentId: '', children: [...] },
//   { id: 2, name: 'Child 1', parentId: 1 },
// ]
```

### Example 3: Handle Deeply Nested Objects

```typescript
const dataList = [
  {
    id: 1,
    name: 'Parent',
    children: [
      {
        id: 2,
        name: 'Child 1',
        children: [
          { id: 3, name: 'Grandchild 1' },
          { id: 4, name: 'Grandchild 2' },
        ],
      },
    ],
  },
];

const result = flatten(dataList, {
  childrenKeyName: 'children',
  parentCreateKeyName: 'parentId',
  idKeyName: 'id',
  parentValue: '',
});
console.log(result);
// Output: [
//   { id: 1, name: 'Parent', parentId: '', children: [...] },
//   { id: 2, name: 'Child 1', parentId: 1, children: [...] },
//   { id: 3, name: 'Grandchild 1', parentId: 2 },
//   { id: 4, name: 'Grandchild 2', parentId: 2 },
// ]
```

### Example 4: Handle Empty Arrays

```typescript
const dataList: any[] = [];

const result = flatten(dataList, { childrenKeyName: 'children' });
console.log(result);
// Output: []
```

## Explanation

1. `Input Validation`: The function ensures dataList is an array and checks if the size parameter is valid.

2. `Flattening Logic`: Uses recursion to handle nested structures. For each object in the array, it adds the object to the result list and processes its children if present.

3. `Parent Reference`: If parentCreateKeyName is provided, the function adds a reference to the parent object in each child.