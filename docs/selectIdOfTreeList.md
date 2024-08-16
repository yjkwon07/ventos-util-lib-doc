---
title: selectIdOfTreeList
sidebar_position: 10
---

# selectIdOfTreeList

The `selectIdOfTreeList` function processes a hierarchical tree structure and generates a list of IDs based on the selected IDs and a specific selection ID. It can include or exclude IDs based on the `isCheck` flag and consider parent-child relationships.

## Function Signature

```ts
const selectIdOfTreeList = <T extends Record<string, any>>(
  treeList: T[],
  {
    selectedIdList,
    idKeyName,
    parentKeyName,
    childrenKeyName,
    selectId,
    isCheck,
  }: {
    selectedIdList: string[];
    idKeyName: KeysOfUnion<T>;
    parentKeyName: KeysOfUnion<T>;
    childrenKeyName: KeysOfUnion<T>;
    selectId: string;
    isCheck: boolean;
  },
): string[];
```

## Parameters

`treeList: T[]`: The hierarchical list of objects to be processed.

`selectedIdList: string[]`: The list of currently selected IDs.

`idKeyName: KeysOfUnion<T>`: The key name for the ID in the objects.

`parentKeyName: KeysOfUnion<T>`: The key name for the parent ID in the objects.

`childrenKeyName: KeysOfUnion<T>`: The key name for the children in the objects.

`selectId`: string: The ID of the node to select or focus on.

`isCheck`: boolean: Flag to determine if the selection should include all descendants of the `selectId`.

## Returns

`string[]`: A list of IDs after processing based on the selection criteria.

## Example Usage

### Example 1: Select Depth ID List When isCheck is True

```typescript
import flatten from './flatten';
import getHierarchyList from './getHierarchyList';

const result = selectIdOfTreeList(treeList, {
  selectedIdList: ['2', '5'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: true,
});

console.log(result);
// Output: ['2', '5', '1', '3']
```

### Example 2: Filter Selected ID List When isCheck is False

```typescript
const result = selectIdOfTreeList(treeList, {
  selectedIdList: ['2', '5'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: false,
});

console.log(result);
// Output: ['5']
```

### Example 3: Handle Empty selectedIdList Gracefully When isCheck is True

```typescript
const result = selectIdOfTreeList(treeList, {
  selectedIdList: [],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: true,
});

console.log(result);
// Output: ['1', '2', '3']
```

### Example 4: Handle Empty treeList Gracefully When isCheck is False

```typescript
const result = selectIdOfTreeList([], {
  selectedIdList: ['2', '5'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: false,
});

console.log(result);
// Output: ['2', '5']
```

### Example 5: Handle Missing selectId in treeList When isCheck is True

```typescript
const result = selectIdOfTreeList(treeList, {
  selectedIdList: ['2', '5'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '10', // Non-existent selectId
  isCheck: true,
});

console.log(result);
// Output: ['2', '5'] // No changes expected since selectId '10' doesn't exist
```

### Example 6: Handle Edge Case with treeList Containing Only selectId When isCheck is True

```typescript
const treeList = [{ id: '1', parentId: '', children: [] }];
const result = selectIdOfTreeList(treeList, {
  selectedIdList: ['2', '5'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: true,
});

console.log(result);
// Output: ['2', '5', '1']
```

### Example 7: Handle Deeply Nested treeList When isCheck is False

```typescript
const treeList = [
  {
    id: '1',
    parentId: '',
    children: [
      {
        id: '2',
        parentId: '1',
        children: [
          { id: '3', parentId: '2', children: [] },
          { id: '4', parentId: '2', children: [] },
        ],
      },
    ],
  },
];

const result = selectIdOfTreeList(treeList, {
  selectedIdList: ['2', '4'],
  idKeyName: 'id',
  parentKeyName: 'parentId',
  childrenKeyName: 'children',
  selectId: '1',
  isCheck: false,
});

console.log(result);
// Output: []
```

## Explanation

1. `Flattening and Hierarchy Extraction`: The function uses the `flatten` utility to convert the selected node and its descendants into a flat list, and `getHierarchyList` to retrieve all parent nodes of the selected node.

2. `ID List Construction`: If `isCheck` is true, the function constructs a list of IDs by including the selected node’s ID and all its descendants, along with parent nodes if all children of the parent are selected. If `isCheck` is false, it filters out IDs not present in the total list.

3. `Edge Cases`: The function handles edge cases such as empty trees, non-existent select IDs, and deeply nested structures gracefully.