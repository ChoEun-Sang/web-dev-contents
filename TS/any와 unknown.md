## any와 unknown

1. any

- 모든 값을 오류없이 받을 수 있다. 즉 타입을 명시하지 않은 것과 동일한 효과
- 타입스크립트 컴파일러 설정: tsconfig.json/noImplicitAny 옵션 활성화 → any 타입 경고 발생
- 어쩔 수 없이 any를 사용해야 할 때 3가지
  - 개발 단계에서 임시로 값을 지정해야 할 때
  - 어떤 값을 받아올지 또는 넘겨줄지 정할 수 없을 때 (타입 파악하기 힘든 외부 라이브러리 등)
  - 값을 예측할 수 없을 때 암묵적으로 사용
- any 사용을 지양하는 이유: 컴파일러에서 에러가 도출되지 않지만, 실제 런타임에서 심각한 오류 발생 가능

1. unknown

- 무엇을 할당할지 어직 모르는 상태의 타입
- 어떤 타입이든 할당 가능하지만, any를 제외한 다른 타입으로 선언된 변수에 unknown 타입 값을 할당할 수 없다.
- 어떤 타입인지 알 수 없기 때문에 함수, 객체 속성 접근, 클래스 생성자 호출을 통한 인스턴스 생성 등 객체 내부 접근시 에러
- 타입 검사를 강제하고 타입 식별된 후에 사용할수 있기 때문에 any보다 안전
