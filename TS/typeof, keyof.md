### 1. `typeof`

`typeof`는 **자바스크립트에서 사용되는 `typeof` 연산자**와 유사하지만, TypeScript에서는 **값의 타입을 추론**하는 데 사용됩니다. 즉, **변수의 타입을 가져와서 다른 곳에서 재사용할 수 있게** 합니다.

#### 예시:

```typescript
const user = {
  name: "John",
  age: 30,
};

type UserType = typeof user;
// UserType는 { name: string; age: number } 타입이 됩니다.
```

이 예시에서 `typeof user`는 객체 `user`의 타입을 추론하고, 그 결과로 `UserType`이라는 타입을 정의할 수 있습니다.

### 2. `keyof`

`keyof`는 **타입의 키(key)들을 문자열 리터럴 타입**으로 반환합니다. 즉, **객체 타입의 속성 이름들을 추출**하는 데 사용됩니다. 주로 **객체의 키를 제한**할 때 유용합니다.

#### 예시:

```typescript
type User = {
  name: string;
  age: number;
};

type UserKeys = keyof User;
// UserKeys는 "name" | "age" 타입이 됩니다.
```

여기서 `keyof User`는 `User` 타입의 키인 `"name"`과 `"age"`를 문자열 리터럴로 반환합니다. 따라서 `UserKeys`는 `"name"` 또는 `"age"`만을 허용하는 타입이 됩니다.

### 요약

- **`typeof`**: 값의 타입을 추론해 타입 정의에 사용할 때 사용.
- **`keyof`**: 객체 타입의 모든 키들을 문자열 리터럴로 반환.

이 두 가지를 조합하면 더욱 강력한 타입 추론과 타입 안전성을 제공할 수 있습니다.
