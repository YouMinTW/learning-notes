## Manipulate item with some similar info

```ts
const data = [
  { name: "iPhone 7", stock: 10, storeDate: "2021/01/01" },
  { name: "iPhone 7", stock: 9, storeDate: "2022/01/01" },
  { name: "iPhone 8", stock: 8, storeDate: "2021/01/01" },
  { name: "iPhone 8", stock: 7, storeDate: "2022/01/01" },
];

function deduplicateTypeToDisplayStrings(rowsData: typeof data): typeof data {
  const productNameMap = new Map<string, undefined>();
  return rowsData.map((row) => {
    if (!productNameMap.has(row.name)) {
      productNameMap.set(row.name, undefined);
      return row;
    }
    return {
      ...row,
      name: "Same above",
    };
  });
}
deduplicateTypeToDisplayStrings(data);
/**
 * [
 *     { name: "iPhone 7", stock: 10, storeDate: "2021/01/01" },
 *     { name: "Same above", stock: 9, storeDate: "2022/01/01" },
 *     { name: "iPhone 8", stock: 8, storeDate: "2021/01/01" },
 *     { name: "Same above", stock: 7, storeDate: "2022/01/01" },
 * ]
 */
```


```js
const data = [
  { name: "Ken", type: "Person" },
  { name: "Dylan", type: "Person" },
  { name: "Tommy", type: "Person" },
  { name: "Biscuit", type: "Pet" },
  { name: "Brandy", type: "Pet" },
];

function mapDataToDisplayList(rowsData) {
  const typeCountMap = new Map();
  return rowsData.map((row) => {
    if (typeCountMap.has(row.type)) {
      typeCountMap.set(row.type, typeCountMap.get(row.type) + 1);
    } else {
      typeCountMap.set(row.type, 1);
    }
    return {
      title: row.name,
      subtitle: `${row.type} ${typeCountMap.get(row.type)}`,
    };
  });
}
mapDataToDisplayList(data);

/**
 * [
 *   { title: 'Ken', subtitle: 'Person 1' },
 *   { title: 'Dylan', subtitle: 'Person 2' },
 *   { title: 'Tommy', subtitle: 'Person 3' },
 *   { title: 'Biscuit', subtitle: 'Pet 1' },
 *   { title: 'Brandy', subtitle: 'Pet 2' }
 * ]
 */
```
