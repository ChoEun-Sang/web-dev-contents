## 'TDZ'란?

> `TDZ`는 Temporal Dead Zone의 약자로, 자바스크립트에서 변수가 선언되기 전에 접근하려고 할 때 발생하는 현상.<br/>
> let, const의 호이스팅이 발생하지만, 해당 변수의 값에 접근할 수 없는 TDZ가 발생하여 참조 에러를 발생시킨다.

> TDZ가 발생하는 이유? <br/>
> 변수는 `선언`, `초기화`, `할당` 거친다.
> var는 선언과 초기화가 동시에 이뤄지며, `undefind`로 초기화.<br/>
> let는 선언, 할당이 각각 진행되고, const는 선언, 할당이 동시에 발생한다.
> let과 const는 초기화되지 않아 반환할 값이 없기 때문에 TDZ 상태에서 에러 발생.

```javascript
// var 의 경우
console.log(a); // undefined
var a = 10;
console.log(a); // 10

// let 의 경우
console.log(b); // ReferenceError: Cannot access 'b' before initialization

let b = 20;
```

- `호이스팅` : 변수와 함수의 선언이 해당 스코프 내의 최상단으로 올라오는 현상

- `초기화`는 변수를 사용하기 전에 값을 할당하는 것. let, const는 초기화 되지 않음
