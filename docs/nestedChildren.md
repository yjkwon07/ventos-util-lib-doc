---
title: nestedChildren
sidebar_position: 8
---

# nestedChildren

These utilities help in transforming flat data structures into nested hierarchical formats. They work with both lists and objects and can include depth information if required.

## createChildrenListByObj

Creates a nested hierarchical structure from a flat data object, adding children and optional depth information.

### Function Signature

```typescript
const createChildrenListByObj = <
  S extends Record<string, T>,
  T extends Record<string, any>,
  K extends string,
  D extends string = '',
>(
  obj: S,
  {
    currentKeyId,
    parentKeyName,
    childrenKeyName,
    depthCreateName,
    depth?: number,
  }: {
    currentKeyId: KeysOfUnion<S>;
    parentKeyName: KeysOfUnion<T>;
    childrenKeyName: K;
    depthCreateName?: D;
    depth?: number;
  },
) => ChildrenNestedObj<T, K, D>;
```

### Parameters

`obj: S`: The data object where keys are IDs and values are data objects.

`currentKeyId`: The ID of the current object to process.

`parentKeyName`: The key name that holds the parent ID.

`childrenKeyName`: The key name where the children will be stored.

`depthCreateName`: Optional key name to store the depth of the current object.

`depth`: The current depth level (default is 0).

### Returns

`ChildrenNestedObj<T, K, D>`: The nested object with children and optional depth information.

## nestedChildrenByList

Transforms a flat list of objects into a hierarchical structure based on parent-child relationships.

### Function Signature

```typescript
export const nestedChildrenByList = <T extends Record<string, any>, P, K extends string, D extends string = ''>(
  list: T[],
  {
    idKeyName,
    parentKeyName,
    childrenKeyName,
    parentValue,
    depthCreateName,
    depth?: number,
  }: {
    idKeyName: KeysOfUnion<T>;
    parentKeyName: KeysOfUnion<T>;
    childrenKeyName: K;
    parentValue: P;
    depthCreateName?: D;
    depth?: number;
  },
) => ChildrenNestedObj<T, K, D>[];
```

### Parameters

`list: T[]`: The flat list of data objects.

`idKeyName`: The key name for the object's unique ID.

`parentKeyName`: The key name for the parent ID.

`childrenKeyName`: The key name where children will be added.

`parentValue`: The value to match for the root parent objects.

`depthCreateName`: Optional key name to store the depth of each object.

`depth`: The initial depth level (default is 0).

### Returns

`ChildrenNestedObj<T, K, D>[]`: The list of nested objects with children and optional depth information.

## nestedChildrenByObj

Transforms a flat data object into a hierarchical structure based on parent-child relationships.

### Function Signature

```typescript
export const nestedChildrenByObj = <T extends Record<string, any>, P, K extends string, D extends string = ''>(
  obj: Record<string | number, T>,
  {
    idKeyName,
    parentKeyName,
    childrenKeyName,
    parentValue,
    depthCreateName,
    depth?: number,
  }: {
    idKeyName: KeysOfUnion<T>;
    parentKeyName: KeysOfUnion<T>;
    childrenKeyName: K;
    parentValue: P;
    depthCreateName?: D;
    depth?: number;
  },
) => ChildrenNestedObj<T, K, D>[];
```

### Parameters

`obj: Record<string | number, T>`: The data object where keys are IDs and values are data objects.

`idKeyName`: The key name for the object's unique ID.

`parentKeyName`: The key name for the parent ID.

`childrenKeyName`: The key name where children will be added.

`parentValue`: The value to match for the root parent objects.

`depthCreateName`: Optional key name to store the depth of each object.

`depth`: The initial depth level (default is 0).

### Returns

`ChildrenNestedObj<T, K, D>[]`: The list of nested objects with children and optional depth information.

### Example Usage

#### nestedChildrenByList

```typescript
const list = [
  { id: 1, name: 'Root', parentId: null },
  { id: 2, name: 'Child 1', parentId: 1 },
  { id: 3, name: 'Child 2', parentId: 1 },
  { id: 4, name: 'Grandchild 1', parentId: 2 },
  { id: 5, name: 'Grandchild 2', parentId: 3 },
];

// Create nested structure
const result = nestedChildrenByList(list, {
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  parentValue: null,
});

console.log(result);
```

#### nestedChildrenByObj

```typescript
const obj = {
  1: { id: 1, name: 'Root', parentId: null },
  2: { id: 2, name: 'Child 1', parentId: 1 },
  3: { id: 3, name: 'Child 2', parentId: 1 },
  4: { id: 4, name: 'Grandchild 1', parentId: 2 },
  5: { id: 5, name: 'Grandchild 2', parentId: 3 },
};

// Create nested structure
const result = nestedChildrenByObj(obj, {
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  parentValue: null,
});

console.log(result);
```