## never 타입

`never` 타입은 TypeScript에서 **절대 발생하지 않는 값**을 나타냅니다. 주로 두 가지 상황에서 사용됩니다:

1. **불가능한 코드 경로**: 어떤 함수나 표현식이 **절대 반환되지 않는 경우** `never` 타입을 사용합니다. 예를 들어, 함수가 무한 루프에 빠지거나 예외를 던져서 정상적으로 종료되지 않는 경우가 해당됩니다.

```typescript
function throwError(message: string): never {
  throw new Error(message); // 예외를 던지기 때문에 함수가 정상적으로 종료되지 않음
}
```

2. **타입이 비어 있는 경우**: TypeScript에서 **빈 유니온 타입을 확인할 때** `never` 타입이 발생할 수 있습니다. 예를 들어, 특정 타입을 좁혔을 때 가능한 값이 없는 경우 `never`로 추론됩니다.

```typescript
function checkType(x: string | number): never {
  if (typeof x === "string") {
    // string 처리
  } else if (typeof x === "number") {
    // number 처리
  }
  // 여기에는 어떤 값도 도달할 수 없으므로 never 타입
}
```

`never`는 안전성을 높여주는 역할을 하며, 코드에서 논리적 오류를 잡는 데 유용합니다.
