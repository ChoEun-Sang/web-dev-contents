## function 함수와 화살표 함수

### Function 함수

- arguments 객체로 함수의 인수에 접근 가능하다
- 함수 호출에 따라 동적으로 this 바인딩. 일반 함수는 호출 시점의 컨텍스트에 따라 this가 달라진다
  - 함수 실행 시 전역 객체 (브라우저: window, node: global), 엄격 모드: undefind (의도치 않게 전역 객체를 참조하는 것을 방지)
  - 메소드 실행 시 메소드를 소유하는 객체
  - 생성자 실행 시 해당 객체
  - call, apply, bind 메소드를 사용하여 this를 변경할 수 있다.
- 생성자 함수로 사용 가능

### 화살표 함수

- 화살표 함수엔 'arguments’가 없습니다
- this 정적으로 바인딩.
  - 화살표 함수가 선언된 렉시컬 스코프(lexical scope)의 this를 가리킨다.
  - 이는 콜백 함수와 같은 상황에서 this 값의 일관성을 유지하려는 목적으로 도입되었다.
  - call, apply, bind 메소드를 사용 불가능
- 생성자 함수로 사용 불가능 (prototype 프로퍼티를 가지고 있지 않기 때문)

### 참고

[화살표 함수 다시 살펴보기](https://ko.javascript.info/arrow-functions)
[화살표 함수와 일반 함수의 차이](https://velog.io/@yjh8806/%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98%EC%99%80-%EC%9D%BC%EB%B0%98-%ED%95%A8%EC%88%98%EC%9D%98-%EC%B0%A8%EC%9D%B4)
