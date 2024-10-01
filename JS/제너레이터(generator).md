# 제너레이터

제너레이터는 이터러블입니다.

제너레이터는 제너레이터 함수를 호출하면 제너레이터 객체를 반환합니다.
제너레이터 객체의 next 매서드를 사용해서 yield 값을 반환합니다. next()를 호출하면 가장 가까운 yield <value>문을 만날 때까지 실행이 지속됩니다(value를 생략할 수도 있는데, 이 경우엔 undefined가 됩니다). 이후, yield <value>문을 만나면 실행이 멈추고 산출하고자 하는 값인 value가 바깥 코드에 반환됩니다. return 만나면 값을 반환하고 종료됩니다.

```js
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

// '제너레이터 함수'는 '제너레이터 객체'를 생성합니다.
let generator = generateSequence();
alert(generator); // [object Generator]
함수 본문 코드는 아직 실행되지 않았습니다.
```

```js
let one = generator.next();
//반환값
{value: 1, done: false};
```

## 비밀번호 만들기

이 함수를 기반으로 좀 더 복잡한 값을 연속해서 생성하는 함수를 만들어봅시다. 값 생성 규칙은 다음과 같습니다.
처음엔 숫자 0부터 9까지를 생성합니다(문자 코드 48부터 57까지),
이어서 알파벳 대문자 A부터 Z까지를 생성합니다(문자 코드 65부터 90까지).
이어서 알파벳 소문자 a부터 z까지를 생성합니다(문자 코드 97부터 122까지).

```js
function* generateSequence(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

function* generatePasswordCodes() {
  // 0..9
  yield* generateSequence(48, 57);

  // A..Z
  yield* generateSequence(65, 90);

  // a..z
  yield* generateSequence(97, 122);
}

let str = "";

for (let code of generatePasswordCodes()) {
  str += String.fromCharCode(code);
}

alert(str); // 0..9A..Za..z
```

다음 챕터에선 for await ... of 루프 안 비동기 데이터 스트림을 다룰 때 사용되는 비동기 제너레이터(asnyc generator)에 대해 알아볼 예정입니다. 비동기 제너레이터는 페이지네이션을 사용해 전송되는 비동기 데이터 스트림을 다룰 때 사용됩니다.

```js
/** 
let count = 0;

for ( let i = a; i <=b, i ++) {
  // 한자리인 경우
  if (b <= 9) return;
  // 2자리 이상일 때
  const arr = Array.from(String(i)); // ex) ["1","1","2"]
  const noDupleArray = new Set(arr)

  if (arr.length === noDupleArray.length) count += 1;
} 
 return count
*/
```
