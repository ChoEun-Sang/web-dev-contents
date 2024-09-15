## Curring

자바스크립트에서 **Currying**은 하나의 함수가 여러 개의 인자를 받는 대신, 각 인자를 하나씩 받는 함수로 변환하는 기법입니다. 쉽게 말해, 여러 개의 인자를 받는 함수를 한 번에 호출하지 않고, 인자를 하나씩 나눠서 호출하는 방식입니다. 이 과정에서 부분적으로 함수가 실행되며, 필요한 인자가 모두 전달되었을 때 최종 결과를 반환합니다.

### 예시:

```javascript
// 일반 함수
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5

// 커링된 함수
function curriedAdd(a) {
  return function (b) {
    return a + b;
  };
}

console.log(curriedAdd(2)(3)); // 5
```

이처럼, `curriedAdd(2)`는 `b` 값을 기다리는 함수가 되고, 그 후에 `b`를 전달받아 결과를 반환하게 됩니다.

### Currying의 장점

- **재사용성**: 특정 인자를 고정하여 부분적으로 실행한 후, 나머지 인자를 다른 곳에서 사용할 수 있습니다.
- **유연성**: 여러 인자를 동시에 전달하거나, 필요에 따라 하나씩 전달할 수 있습니다.

### 실전 예시 (함수 조합):

```javascript
const multiply = (a) => (b) => a * b;
const double = multiply(2);

console.log(double(5)); // 10
```

이 예시에서 `double`은 항상 2를 곱하는 함수로 사용할 수 있습니다. Currying을 통해 함수의 재사용성을 높일 수 있죠.
