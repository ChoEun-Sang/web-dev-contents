## this

- 객체를 가리키는 키워드
- 함수를 호출한 객체

- 전역 문맥에서 this

  - 브라우저 전역 객체: window
  - example 함수에서 this는 window

- 엄격 모드에서 this (use strict) : 내가 사용하는 자바스크립트 문법을 엄격하게 검사

  - 브라우저 전역 객체: window
  - example 함수에서 this는 undefined
  - 객체를 지정해야 this가 생긴다.

- 호출한 객체에 따라 동적으로 객체가 바뀌는 this

```js
const object = {
  name: "foo",
  main: function () {
    console.log(this);
  },
};

object.main(); // => "foo"

const main2 = object.main;
main2.main(); // => window
```

- bind 매서드
  - bind를 중복해서 적용 안 됨

```js
function main() {
  console.log(this);
}

const mainBain = main.bind({ nane: "hi" });

const object = {
  name: "foo",
  mainBain,
};

object.mainBain(); // => { nane: "hi" }
```
