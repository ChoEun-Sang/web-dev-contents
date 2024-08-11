## useEffect

`useEffect`는 순수한 리액트 컴포넌트 내에서 **사이드 이펙트**를 처리합니다.

> useEffect( callback, [의존성 배열])

- state나 props가 변경될 때 실행하고 싶다면,

```js
useEffect(() => {
  // 의존성 배열에 특정 값을 넣는다.
}, [count]);
```

- Componet가 처음 랜더링 됐을 때 한 번 실행하고 싶다면, 의존성 배열을 빈 배열로 설정한다.

```js
useEffect(() => {
  // 의존성 배열을 빈 배열로 설정
}, []);
```

- 배열을 생략하면 리렌더링 될 떄마다 실행된다.

```js
useEffect(() => {
  // 의존성 배열을 생략
});
```

- clean up Fn

  - 컴포넌트가 unmount 되기 직전에 실행되는 함수
  - 타이머 함수, 네트워크 요청, mount된 상태 구독 해제
  - return () => {}

- clean up 함수가 발생하는 시점

  - 컴포넌트가 리랜더링 되기 전, 즉, 컴포넌트가 unmount되기 직전에 clean up 함수 실행됩니다.
  - 그리고 새롭게 컴포넌트가 mount 되면서 useEffect가 실행된다.

  - 예시

  ```jsx
  function example() {
    const [count, setCount] = useState(0);

    useEffect(() => {
      console.log(count, "mount");
      return () => {
        console.log(count, "unmount");
      };
    }, [count]);
  }

  // 0, "unmount"
  // 1, "mount"
  ```

  ### 용어 정리

  > **사이드 이펙트**
  >
  > - 백엔드 서버로부터 데이터를 요청
  > - `document`나 `window`와 같은 브라우저 API와의 상호작용
  > - `setTimeout` 또는 `setInterval`과 같은 타이밍 함수 사용

  > **순수 함수(pure function)**
  >
  > - 함수의 리턴 값이 동일한 인수(argument)에 대해 동일하다.
  > - side effect가 없다. (외부의 상태를 변경하지 않는다.)
