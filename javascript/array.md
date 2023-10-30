## Manipulate item some similar info

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
