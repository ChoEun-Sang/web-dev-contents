## arguments 객체

function 함수와 화살표 함수 차이를 설명할 때, arguments 객체 사용 가능 여부에 대해서 나와서 알아보았다.

arguments 객체는 모든 함수 내에서 이용 가능한 지역 변수이다. 함수의 인자를 Array 형태로 갖는 객체이다.
argumentss 객체를 사용하여 함수 내에서 모든 인수를 참조할 수 있으며, 호출할 때 제공한 인수 각각에 대한 항목을 갖고 있다. 항목의 인덱스는 0부터 시작한다.

```js
function func1(a, b, c) {
  console.log(arguments);
  // ["apple", "bee", "cat"]
}

func1("apple", "bee", "cat");
```

```js
function func1(a, b, c) {
  console.log(arguments[0]);
  // Expected output: 1

  console.log(arguments[1]);
  // Expected output: 2

  console.log(arguments[2]);
  // Expected output: 3
}

func1(1, 2, 3);
```

> 참고 1. "Array 형태"란 arguments가 length 속성과 더불어 0부터 인덱스 된 다른 속성을 가지고 있지만, Array의 forEach, map과 같은 내장 메서드를 가지고 있지 않다는 뜻입니다.

> 참고 2. 화살표 함수는 arguments 객체를 가지고 있지 않는다.
