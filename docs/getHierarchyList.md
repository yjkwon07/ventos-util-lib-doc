---
title: getHierarchyList
sidebar_position: 7
---

# getHierarchyList

The `getHierarchyList` function retrieves a list of hierarchical objects starting from a specified target object and including all its ancestors up to the root. It gracefully handles cases where the target object has no parents or if the hierarchy contains circular references.

## Function Signature

```typescript
const getHierarchyList = <T, C extends { [key: string]: any }>(
  hierarchyList: C[],
  { idKeyName, parentKeyName, targetId }: { idKeyName: string; parentKeyName: string; targetId: T },
): C[];
```

## Parameters

`hierarchyList: C[]`: An array of objects representing the hierarchical data.

`idKeyName: string`: The key name used to identify each object uniquely.

`parentKeyName: string`: The key name used to reference the parent of each object.

`targetId: T`: The ID of the target object from which the hierarchy should be retrieved.

## Returns

`C[]`: A list of objects representing the target object and its ancestors up to the root.

## Example Usage

### Example 1: Retrieve Hierarchy Up to the Root

```typescript
const dataList = [
  { id: 1, name: 'Root', parentId: null },
  { id: 2, name: 'Child 1', parentId: 1 },
  { id: 3, name: 'Child 2', parentId: 1 },
  { id: 4, name: 'Grandchild 1', parentId: 2 },
  { id: 5, name: 'Grandchild 2', parentId: 3 },
  { id: 6, name: 'Great-Grandchild 1', parentId: 4 },
];

const result = getHierarchyList(dataList, { idKeyName: 'id', parentKeyName: 'parentId', targetId: 6 });
console.log(result);
// Output: [
//   { id: 6, name: 'Great-Grandchild 1', parentId: 4 },
//   { id: 4, name: 'Grandchild 1', parentId: 2 },
//   { id: 2, name: 'Child 1', parentId: 1 },
//   { id: 1, name: 'Root', parentId: null },
// ]
```

### Example 2: Retrieve Category with No Parents

```typescript
const result = getHierarchyList(dataList, { idKeyName: 'id', parentKeyName: 'parentId', targetId: 1 });
console.log(result);
// Output: [{ id: 1, name: 'Root', parentId: null }]
```

### Example 3: Handle Target ID Not Found

```typescript
const result = getHierarchyList(dataList, { idKeyName: 'id', parentKeyName: 'parentId', targetId: 99 });
console.log(result);
// Output: []
```

### Example 4: Handle Category with No Children

```typescript
const result = getHierarchyList(dataList, { idKeyName: 'id', parentKeyName: 'parentId', targetId: 5 });
console.log(result);
// Output: [
//   { id: 5, name: 'Grandchild 2', parentId: 3 },
//   { id: 3, name: 'Child 2', parentId: 1 },
//   { id: 1, name: 'Root', parentId: null },
// ]
```

### Example 5: Handle Circular References

```typescript
const circularDataList = [
  { id: 1, name: 'Root', parentId: 3 },
  { id: 2, name: 'Child 1', parentId: 1 },
  { id: 3, name: 'Child 2', parentId: 2 },
];

const result = getHierarchyList(circularDataList, { idKeyName: 'id', parentKeyName: 'parentId', targetId: 3 });
console.log(result);
// Output: [
//   { id: 3, name: 'Child 2', parentId: 2 },
//   { id: 2, name: 'Child 1', parentId: 1 },
//   { id: 1, name: 'Root', parentId: 3 },
// ]
```

## Explanation

1. `Input Parameters`: The function uses `idKeyName` to identify each object, parentKeyName to find parent references, and `targetId` to start the hierarchy retrieval.

2. `Hierarchy Retrieval`: The function traverses up the hierarchy from the target object, collecting each ancestor until it reaches the root or a previously visited object.

3. `Circular References`: The function handles circular references by using a `Set` to keep track of visited objects, preventing infinite loops.