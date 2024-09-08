## enum

- 열거형, 여러 값들에 미리 이름을 정의하여 열거해두고 사용하는 타입
- 관련이 높은 멤버를 모아 문자열 상수처럼 사용하고자 할때 유용하게 쓸 수 있다.
- enum은 선언한 값을 외부에서 변경할 수 없다.
- 숫자 상수로 관리하는 열거형은 선언한 값 이외의 값을 할당하거나 접근해도 에러를 발생시키지 않기 때문에 숫자 상수는 사용하지 않는 것을 권장한다.
- 역방향으로 접근했을 때 오류를 내지 않는다. 대신 const enum는 역방향 접근을 허용하지 않는다.
- js에서 객체를 사용해서 enum과 비슷하게 구현할 수 있지만, `key`, `value`가 변경될 수 있다.

```js
// 값을 지정하지 않으면 0부터 숫자를 매긴다.
  enum Artist{
    beyonce, // 0
    tyla, // 1
    ladygaga, // 2
    taylorSwift, // 3
    brunoMars, // 4

  }


    enum Artist {
    beyonce = "beyonce",
    tyla = "tyla",
    ladygaga = "ladygaga",
    taylorSwift = "taylorSwift",
    brunoMars = "brunoMars",
  }
```

### enum 필요성

- 종류를 정의하여 명확한 사용과 가독성의 증가
- 하드 코딩으로 인한 실수를 줄이기 위함

```js
// 하드 코딩
export const whichSongDoyYouLike = (artist: string) => {
  switch (artist) {
    case "beyonce":
      console.log("single lady");
      break;
    case "tyla":
      cosole.log("warter");
      break;
    default:
      console.log("원하는 가수가 없어요");
      break;
  }
};

// enum 사용
export const whichSongDoyYouLike = (artist: string) => {
  switch (artist) {
    case Artist.beyonce:
      console.log("single lady");
      break;
    case Artist.tyla:
      cosole.log("warter");
      break;
    default:
      console.log("원하는 가수가 없어요");
      break;
  }
};
```

### enum의 문제점

- Tree Shacking이 되지 않는다.

> _JavaScript에 존재하지 않는 것을 구현하기 위해 TypeScript 컴파일러는 IIFE(즉시 실행 함수)를 포함한 코드를 생성한다. 하지만 Rollup 과 같은 번들러는 IIFE를 '사용하지 않는 코드'라고 판단할 수 없어서 Tree-shaking이 되지 않는다. 결국 위의 예제의 OsType을 import하고 실제로 사용하지 않더라도 최종 번들에는 포함되는 것이다._

```js
// Enum을 JS로 트랜스파일하면,

// 값 지정하지 않는 경우,
export var Artist;
(function (Artist) {
  Artist[(Artist["beyonce"] = 0)] = "beyonce";
  Artist[(Artist["tyla"] = 1)] = "tyla";
  Artist[(Artist["ladygaga"] = 2)] = "ladygaga";
  Artist[(Artist["taylorSwift"] = 3)] = "taylorSwift";
  Artist[(Artist["brunoMars"] = 4)] = "brunoMars";
})(Artist || (Artist = {}));

// 문자열을 할당한 경우,
export var Artist;
(function (Artist) {
  Artist["beyonce"] = "beyonce";
  Artist["tyla"] = "tyla";
  Artist["ladygaga"] = "ladygaga";
  //...중략
})(Artist || (Artist = {}));
```

### 개선 방안

1. as const assertion을 사용해서 Union Type의 사용 (추천)

- 사용할 수 있는 요소들을 지정해서 지정된 값만 사용할 수 있도록 한다.

````js
const Artist = {
    beyonce = "beyonce1",
    tyla = "tyla2",
    ladygaga = "ladygaga3",
    taylorSwift = "taylorSwift4",
    brunoMars = "brunoMars5",
} as const

type Key = keyof typeof Artist; // type Artist = "beyonce" | "tyla" | "ladygaga" | "taylorSwift" | "brunoMars" ;
type Value = (typeof Artist)[Key]; // type Value = "beyonce1" | "tyla2" | "ladygaga3" | "taylorSwift4" | "brunoMars5" ;

2. const enum의 사용

- 순수 enum보다 더 간결하고 IIFE를 사용하지 않으니, Tree-shaking도 가능하다.
- 문제점: `--isolatedModules`가 켜져있다면 const enum의 값을 외부에서 읽을 수 없다.

```js
const enum Artist{
    beyonce = "beyonce",
    tyla = "tyla",
    ladygaga = "ladygaga",
    taylorSwift = "taylorSwift",
    brunoMars = "brunoMars",
  }

const tyla = Artist.tyla // => const tyla = "tyla"
````

## 참고

[[TypeScript] Enum이란](https://velog.io/@ahsy92/TypeScript-Enum이란)
