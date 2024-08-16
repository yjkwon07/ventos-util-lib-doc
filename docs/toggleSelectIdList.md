---
title: toggleSelectIdList
sidebar_position: 13
---

# toggleSelectIdList

The `toggleSelectIdList` function is used to add or remove an item from a list based on a boolean flag. This is useful for managing selections, such as adding or removing items from a list of selected items.

## Function Signature

```ts
const toggleSelectIdList = <T>(selectList: T[], { selectId, isChecked }: { selectId: T; isChecked: boolean }) => T[];
```

## Parameters

`selectList: T[]`: The current list of selected items.

`selectId: T`: The item to add or remove from the selectList.

`isChecked: boolean`: If true, the item is added to the list. If false, the item is removed from the list.

## Returns

`T[]`: The updated list of selected items.

## Example Usage

### Example 1: Adding an Item to the List

```typescript
const selectList = [1, 2, 3];
const updatedList = toggleSelectIdList(selectList, { selectId: 4, isChecked: true });
console.log(updatedList);
// Output: [1, 2, 3, 4]
```

### Example 2: Removing an Item from the List

```typescript
const selectList = [1, 2, 3, 4];
const updatedList = toggleSelectIdList(selectList, { selectId: 3, isChecked: false });
console.log(updatedList);
// Output: [1, 2, 4]
```

### Example 3: Attempting to Add an Item That Already Exists

```typescript
const selectList = [1, 2, 3];
const updatedList = toggleSelectIdList(selectList, { selectId: 2, isChecked: true });
console.log(updatedList);
// Output: [1, 2, 3, 2]
```

### Example 4: Attempting to Remove an Item That Is Not in the List

```typescript
const selectList = [1, 2, 3];
const updatedList = toggleSelectIdList(selectList, { selectId: 4, isChecked: false });
console.log(updatedList);
// Output: [1, 2, 3]
```

## Explanation

1. `Adding an Item`: When isChecked is true, the function appends the selectId to the selectList. If the item is already in the list, it will be duplicated in the result.

2. `Removing an Item`: When isChecked is false, the function removes the selectId from the selectList. If the item is not in the list, the list remains unchanged.

3. `Handling Duplicates`: When adding an item, if the item already exists in the list, it will be added again, leading to duplicates.

4. `Handling Non-Existent` Items: When removing an item, if the item does not exist in the list, the function simply returns the original list.