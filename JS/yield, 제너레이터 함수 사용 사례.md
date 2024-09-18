## yield, 제너레이터 함수 사용 사례

`yield`와 제너레이터 함수는 자바스크립트에서 **비동기 처리** 또는 **대량의 데이터를 효율적으로 처리**할 때 매우 유용한 기능입니다. `function*` 키워드를 사용해 제너레이터 함수를 정의하고, `yield` 키워드를 사용해 함수 실행을 중단하고 나중에 다시 실행을 재개할 수 있습니다.

### `yield`와 제너레이터 함수 기본 개념

제너레이터 함수는 일반 함수와 다르게 **실행이 중단**될 수 있으며, 필요할 때마다 실행을 재개할 수 있습니다. `yield` 키워드는 **값을 반환하면서 함수의 실행을 중지**하는 역할을 하고, 나중에 그 위치에서 다시 시작할 수 있게 해줍니다.

#### 기본 예시

```javascript
function* myGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = myGenerator();

console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

위 예시에서는 `gen.next()`를 호출할 때마다 제너레이터 함수가 `yield`를 만나 실행을 중지하고, 그 값을 반환합니다.

### 제너레이터 함수 사용 사례

#### 1. **이터레이터 구현**

제너레이터 함수는 이터레이터 패턴을 구현할 때 많이 사용됩니다. 특히, 무한한 데이터나 큰 데이터를 순차적으로 처리할 때 효율적입니다.

```javascript
function* infiniteNumbers() {
  let num = 1;
  while (true) {
    yield num++;
  }
}

const numbers = infiniteNumbers();
console.log(numbers.next().value); // 1
console.log(numbers.next().value); // 2
console.log(numbers.next().value); // 3
// 계속해서 호출할 때마다 숫자가 증가
```

위 코드에서 `infiniteNumbers()`는 무한한 숫자를 생성할 수 있는 이터레이터로 동작하며, 필요할 때마다 값을 생성합니다. 이 방식은 **무한한 양의 데이터**를 효율적으로 다룰 수 있습니다.

#### 2. **비동기 흐름 제어 (async-await 이전)**

`async-await`이 등장하기 전에는 `yield`를 사용하여 비동기 작업을 제어하는 방식이 많이 사용되었습니다. 예를 들어, AJAX 요청을 순차적으로 처리하거나 비동기 코드에서 콜백 지옥을 방지할 때 유용했습니다.

```javascript
function* fetchData() {
  const user = yield fetch("https://jsonplaceholder.typicode.com/users/1").then(
    (res) => res.json()
  );
  console.log(user);
  const posts = yield fetch(
    "https://jsonplaceholder.typicode.com/posts?userId=1"
  ).then((res) => res.json());
  console.log(posts);
}

const iterator = fetchData();
iterator.next().value.then((user) => {
  iterator.next(user).value.then((posts) => {
    iterator.next(posts);
  });
});
```

위 예시에서는 `fetch`를 사용하여 데이터를 가져오고, `yield`로 비동기 작업을 제어합니다. 비록 `async-await`이 등장하면서 더 직관적인 방식으로 대체되었지만, 제너레이터를 사용한 비동기 제어는 여전히 이해할 만한 가치가 있습니다.

#### 3. **대량 데이터 처리**

제너레이터는 큰 데이터 집합을 처리할 때 메모리 효율성을 극대화할 수 있습니다. 모든 데이터를 한꺼번에 메모리에 로드하지 않고, 필요한 만큼만 순차적으로 처리할 수 있기 때문입니다.

```javascript
function* bigDataProcessor(data) {
  for (let i = 0; i < data.length; i++) {
    yield data[i]; // 데이터 하나씩 처리
  }
}

const bigData = new Array(10000).fill().map((_, i) => i); // 10,000개의 데이터
const processor = bigDataProcessor(bigData);

for (let i = 0; i < 5; i++) {
  console.log(processor.next().value); // 필요한 만큼만 처리
}
```

이 예시에서는 10,000개의 데이터 중 처음 5개만 처리하는 식으로 동작합니다. 전체 데이터를 메모리에 한 번에 올리지 않고 필요한 만큼만 처리할 수 있어 효율적입니다.

#### 4. **상태 유지 및 간단한 작업 관리**

제너레이터는 상태를 쉽게 유지할 수 있기 때문에, 상태 기반 시스템이나 순차적인 작업 처리가 필요한 곳에서 사용됩니다. 예를 들어, 간단한 상태 머신 구현도 가능합니다.

```javascript
function* stateMachine() {
  yield "state 1";
  yield "state 2";
  yield "state 3";
}

const states = stateMachine();
console.log(states.next().value); // state 1
console.log(states.next().value); // state 2
console.log(states.next().value); // state 3
```

이런 구조를 통해 특정 상태를 가지며 각 단계에서 그 상태를 관리하는 방식으로 동작할 수 있습니다.

### 요약

`yield`와 제너레이터 함수의 사용 사례는 다음과 같습니다:

- **이터레이터 구현**: 무한 데이터나 큰 데이터를 순차적으로 처리.
- **비동기 흐름 제어**: 비동기 작업을 직관적으로 제어.
- **대량 데이터 처리**: 메모리 효율성을 위해 큰 데이터를 부분적으로 처리.
- **상태 유지 및 작업 관리**: 상태 머신처럼 단계별 상태 관리.

제너레이터는 특히 **효율적인 데이터 처리**와 **복잡한 비동기 작업** 관리에 매우 유용한 도구입니다.
