## exhaustiveness checking으로 정확한 타입 분기하기

모든 케이스에 대해 철저하게 타입 검사하기

```js
type Discount = "1000" | "2000" | "3000";

const getProductNage = (discount: Discount): string => {
  if (discount === "1000") return "1000원 할인";
  if (discount === "2000") return "2000원 할인";
  // if (discount ==="3000") return "3000원 할인";
  else {
    exhaustiveCheck(discount); // Error: Argument of type 'string' is not assign able to parameter of type 'never';
    return "꽝";
  }
};

const exhaustiveCheck = (param: never) => {
  throw new Error("Type Error");
};
```
