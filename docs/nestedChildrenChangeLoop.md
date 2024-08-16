---
title: nestedChildrenChangeLoop
sidebar_position: 9
---

# nestedChildrenChangeLoop

The `nestedChildrenUpdateLoop` function allows you to traverse a nested object structure and apply a callback function to each object within the structure. This can be useful for deep updates or transformations.

## Function Signature

```ts
const nestedChildrenUpdateLoop = <T extends { [key: string]: any }, R extends T>(
  obj: R,
  {
    childrenKeyName,
    updateCallback,
  }: {
    childrenKeyName: string;
    updateCallback: (findObj: T, parentObj: R | null) => Partial<R>;
  },
): R;
```

## Parameters

`obj`: R: The root object of the nested structure that will be traversed and updated.

`childrenKeyName: string`: The key name that holds child elements within each object.

`updateCallback: (findObj: T, parentObj: R | null) => Partial<R>`: A callback function that is called for each object found during the traversal. It takes the current object and its parent object, returning a partial object to update the current object.

## Returns

`R`: The updated root object with all nested objects transformed according to the updateCallback.

## Example Usage

### Example 1: Apply Callback to Each Nested Object

```typescript
const obj = {
  id: 1,
  name: 'Root',
  children: [
    {
      id: 2,
      name: 'Child 1',
      children: [
        {
          id: 4,
          name: 'Grandchild 1',
          children: [],
        },
      ],
    },
    {
      id: 3,
      name: 'Child 2',
      children: [
        {
          id: 5,
          name: 'Grandchild 2',
          children: [],
        },
      ],
    },
  ],
};

const result = nestedChildrenUpdateLoop(obj, {
  childrenKeyName: 'children',
  updateCallback: (item) => {
    return { ...item, name: `${item.name} Modified` };
  },
});

console.log(result);
// Output: {
//   id: 1,
//   name: 'Root Modified',
//   children: [
//     {
//       id: 2,
//       name: 'Child 1 Modified',
//       children: [
//         {
//           id: 4,
//           name: 'Grandchild 1 Modified',
//           children: [],
//         },
//       ],
//     },
//     {
//       id: 3,
//       name: 'Child 2 Modified',
//       children: [
//         {
//           id: 5,
//           name: 'Grandchild 2 Modified',
//           children: [],
//         },
//       ],
//     },
//   ],
// }
```

### Example 2: Apply Callback to Selected Properties Based on Condition

```typescript
const result = nestedChildrenUpdateLoop(obj, {
  childrenKeyName: 'children',
  updateCallback: (item) => {
    if (item.id === 4) {
      return { ...item, name: `${item.name} Modified` };
    }
    return item;
  },
});

console.log(result);
// Output: {
//   id: 1,
//   name: 'Root',
//   children: [
//     {
//       id: 2,
//       name: 'Child 1',
//       children: [
//         {
//           id: 4,
//           name: 'Grandchild 1 Modified',
//           children: [],
//         },
//       ],
//     },
//     {
//       id: 3,
//       name: 'Child 2',
//       children: [
//         {
//           id: 5,
//           name: 'Grandchild 2',
//           children: [],
//         },
//       ],
//     },
//   ],
// }
```

### Example 3: Handle Objects with No Children

```typescript
const singleObj = {
  id: 1,
  name: 'Single',
  children: [],
};

const result = nestedChildrenUpdateLoop(singleObj, {
  childrenKeyName: 'children',
  updateCallback: (item) => {
    return { ...item, name: `${item.name} Modified` };
  },
});

console.log(result);
// Output: {
//   id: 1,
//   name: 'Single Modified',
//   children: [],
// }
```

### Example 4: Ensure Original Object Is Not Mutated

```typescript
const originalObj = {
  id: 1,
  name: 'Root',
  children: [
    {
      id: 2,
      name: 'Child 1',
      children: [
        {
          id: 4,
          name: 'Grandchild 1',
          children: [],
        },
      ],
    },
    {
      id: 3,
      name: 'Child 2',
      children: [
        {
          id: 5,
          name: 'Grandchild 2',
          children: [],
        },
      ],
    },
  ],
};

const result = nestedChildrenUpdateLoop(originalObj, {
  childrenKeyName: 'children',
  updateCallback: (item) => {
    return { ...item, name: `${item.name} Modified` };
  },
});

console.log(originalObj);
// Output: {
//   id: 1,
//   name: 'Root',
//   children: [
//     {
//       id: 2,
//       name: 'Child 1',
//       children: [
//         {
//           id: 4,
//           name: 'Grandchild 1',
//           children: [],
//         },
//       ],
//     },
//     {
//       id: 3,
//       name: 'Child 2',
//       children: [
//         {
//           id: 5,
//           name: 'Grandchild 2',
//           children: [],
//         },
//       ],
//     },
//   ],
// }

console.log(result);
// Output: {
//   id: 1,
//   name: 'Root Modified',
//   children: [
//     {
//       id: 2,
//       name: 'Child 1 Modified',
//       children: [
//         {
//           id: 4,
//           name: 'Grandchild 1 Modified',
//           children: [],
//         },
//       ],
//     },
//     {
//       id: 3,
//       name: 'Child 2 Modified',
//       children: [
//         {
//           id: 5,
//           name: 'Grandchild 2 Modified',
//           children: [],
//         },
//       ],
//     },
//   ],
// }
```

## Explanation

`Input Validation`: The function ensures `obj` is a valid object and checks that the `childrenKeyName` is a string.

`Traversal and Update Logic`: The function uses recursion to traverse the object tree. For each object, it applies the `updateCallback` and updates the object. If an object has children, it recursively processes each child.

`Cloning`: The function uses `lodash/cloneDeep` to create a deep copy of the object before applying any updates to ensure the original object remains unaltered.