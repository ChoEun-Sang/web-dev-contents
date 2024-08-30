## 랜더링 최적화

### frame per second

모니터 주사율은 1초동안 화면 출련 빈도를 나타내는 단위입니다. hz 단위를 사용하는데, hz는 frame과 연관이 있습니다. 우리가 영화를 볼 때, 초당 몇 프레임이 보여지는지에 따라 움직임의 자연스러움이 달라집니다.
인간의 눈은 보통 1초에 60번의 프레임이 보여져야 자연스럽게 보인다고 해서, 보통 초당 60 프레임이 그려지도록 설계합니다. 이를 60fps 혹은 60hz 표현합니다.

자연스러운 애니메이션을 구현하려면 1000ms/60fps = 16.6ms 간격마다 코드를 호출해야 한다는 것입니다.

### setTimeout, setInterval

웹 사이트의 애니메이션을 구현할 때, transition 과 같은 CSS 를 이용해서 애니메이션을 구현하거나,
Javascript를 사용해서 좀더 복잡한 애니메이션을 구현합니다.

Javascript를 이용한 애니메이션은 setTimeout(), setInterval() 타이머 함수를 사용해서 사용자가 지정한 시간에 따라 애니메이션을 발생시킬 수 있습니다. 하지만, 타이머 함수는 프레임 단위로 프레임 시작 시간에 맞춰 실행됨을 보장하지 못하기 때문이다.

자바스크립트 엔진은 싱글 스레드로 하나의 콜스택으로 작업을 처리하기 때문에, 콜스택이 처리해야 할 작업량이 많을 경우, 약 16ms 간격으로 프레임 단위가 진행되지 못할 수 있습니다.
콜백 함수가 16ms 중간에 실행되어 자바스크립트 실행에 의해 리플로우 현상이 다시 일어날 수 있습니다.
그러면 프레임 생성되지 못하고 1 프레임이 생략되는 현상이 발생해서 화면이 자연스럽지 못하게 됩니다.

```js
const animation = () => {
  // 애니메이션
};

setInterval(animation, 1000 / 60);
```

### requestAnimationFrame

requestAnimationFrame 를 통해 애니메이션을 구현할 때, 각 프레임이 브라우저의 프레임 주기에 맞추어 일정한 시간 간격으로 렌더링됩니다. 지연 및 블로킹 현상이 생기지 않아 보다 부드러운 애니메이션을 제공합니다.

#### requestAnimationFrame 사용법

requestAnimationFrame 사용법은 setTimeout 처럼 콜백 함수 내부에서 재귀 호출 하는 식으로 구성하면 됩니다. 차이점은 setTimeout 은 타이머를 지정해주어야 하지만, requestAnimationFrame 은 프레임 단위로 동작하기 때문에 별도의 반복 플래그가 필요 없다는 점입니다.
그리고 setTimeout 을 취소하기 위해 clearTimout 을 사용하듯이, requestAnimationFrame 를 취소하는 방법으로 cancelAnimationFrame 를 사용한다. 아래와 같이 특정한 조건에서 애니메이션을 중지하고 싶을때 이용하면 된다.

```js
let raf; // requestAnimationFrame을 담을 변수

const performAnimation = () => {
  /* 스타일 조정 스크립트 */

  // 특정한 조건일 경우 raf를 중지하고 콜백 종료
  if (조건) {
    cancelAnimationFrame(raf);
    return;
  }

  raf = requestAnimationFrame(performAnimation); // 함수 내부에서 다시 requestAnimationFrame을 호출하여 반복
};

requestAnimationFrame(performAnimation);
```

#### 애니메이션 타이머 이용하기

requestAnimationFrame 함수의 콜백 함수의 인자로 매개변수를 전달하면 requestAnimationFrame 함수가 실행되기 시작한 이후의 시간을 얻을 수 있습니다. 이를 이용해 애니메이션 수행 시간을 구해 특정 타이머일때 스크립트를 실행하는 식의 응용이 가능합니다.

```js
let startTime;

// requestAnimationFrame의 콜백 함수에 매개변수를 정의
const draw = (timestamp) => {
  if (!start) start = timestamp; // 애니메이션 시작 시간

  currentTime = timestamp - startTime;

  // 애니메이션이 실행된지 2초가 지나면..
  if (currentTime > 2000) {
    console.log("END");
    return;
  }

  requestAnimationFrame(draw);
};

requestAnimationFrame(draw);
```

## 출처

[웹 애니메이션 최적화 requestAnimationFrame 가이드](https://inpa.tistory.com/entry/%F0%9F%8C%90-requestAnimationFrame-%EA%B0%80%EC%9D%B4%EB%93%9C)
