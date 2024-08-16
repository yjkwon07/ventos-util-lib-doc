---
title: toggleSelectItemList
sidebar_position: 14
---

# toggleSelectItemList

The `toggleSelectItemList` function adds or removes an item from a list of objects based on a specified key and a boolean flag. If the flag `isChecked` is `true`, the function adds the item to the list if it isn't already present. If `isChecked` is `false`, the function removes the item from the list if it exists.

## Function Signature

```typescript
const toggleSelectItemList = <T extends { [key: string]: any }>(
  selectItemList: T[],
  { selectItem, idKeyName, isChecked }: { selectItem: T; idKeyName: string; isChecked: boolean },
) => T[];
```

## Parameters

`selectItemList: T[]`: The current list of selected items.

`selectItem: T`: The item to add or remove.

`idKeyName`: string: The key used to uniquely identify items in the list.

`isChecked`: boolean: Determines whether to add or remove the item.

## Returns

`T[]`: The updated list of selected items.

## Example Usage

### Adding an Item

```typescript
const selectItemList = [{ id: 1 }, { id: 2 }];
const selectItem = { id: 3 };
const updatedList = toggleSelectItemList(selectItemList, { selectItem, idKeyName: 'id', isChecked: true });
console.log(updatedList);
// Output: [{ id: 1 }, { id: 2 }, { id: 3 }]
```

### Removing an Item

```typescript
const selectItemList = [{ id: 1 }, { id: 2 }, { id: 3 }];
const selectItem = { id: 2 };
const updatedList = toggleSelectItemList(selectItemList, { selectItem, idKeyName: 'id', isChecked: false });
console.log(updatedList);
// Output: [{ id: 1 }, { id: 3 }]
```

## Edge Cases

1. `Duplicate Items`: If the item already exists in the list, adding it again will not create a duplicate.

2. `Non-Existent Items`: Removing an item that is not in the list will not affect the list.

3. `Different Key Names`: The function handles different key names used for identification.