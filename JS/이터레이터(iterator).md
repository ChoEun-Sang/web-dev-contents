## 이터레이터

이터레이터는 이터러블 객체의 요소를 하나씩 순회하는 객체입니다. next 매서드를 통해 계속 다음 값을 반환하고, 순회가 끝나면 done: false를 반환합니다.

이터러블한 객체는 range 객체에 Symbol.iterator 키가 있습니다.
for...of 문을 실행하면, Symbol.iterator가 호출되면서 iterator 객체를 반환합니다.
iterator 객체는 next()를 사용해서 계속 { value: any, done: false } 형태의 다음 값을 반환하고, 순환이 끝나면 done: false를 반환합니다.

### 일반 객체를 이터러블 객체로 만들기

```js
const range = { from: 1, to: 5 };

range[Symbol.iterator] = function () {
  return {
    current: this.from,
    last: this.to,
    next() {
      if (this.current <= this.last) {
        return {
          value: this.current++,
          done: false,
        };
      } else {
        return {
          done: true,
        };
      }
    },
  };
};

for (let num of range) {
  console.log(num);
}
```

### 이터레이터 명시적으로 호출하기

이터레이터를 명시적으로 호출하는 경우는 거의 없지만, for..of보다 반복을 통제할 수 있다는 장점이 있다.

```js
const rangeIterator = range[Symbol.iterator]();

while (true) {
  const result = rangeIterator.next();
  if (result.done) break;

  console.log(result);
}
```

### 이터러블과 유사배열

- 이터러블은 Symbol.iterator가 구현된 객체입니다.
- 유사 배열은 인덱스와 length가 있어서 배열처럼 보이는 객체입니다.
- 이터러블객체이면서 유사 배열은 문자열. 숫자 인덱스와 length 프로퍼티가 있음.

## Array.from

map과 push, pop 과 같은 배열 매서드를 사용하려면 배열이어야 합니다.
Array.from는 iterable 객체나 유사 배열을 Array로 만듭니다.
새로운 배열을 만들고 객체의 모든 요소를 새롭게 만든 배열로 복사합니다.

```js
Array.from(obj[, mapFn, thisArg])
```
