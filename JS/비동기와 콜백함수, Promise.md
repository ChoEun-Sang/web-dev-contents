## 비동기

특정 작업이 완료될 때까지 기다리지 않고, 다음 작업을 수행할 수 있는 방식입니다. 여러가지 일을 동시에 처리하는 것 처럼 보이지만, 실제로 컴퓨터가 짧은 시간 동안 빠르게 번갈아 가며 처리하는 것입니다.

## 콜백 함수

비동기 작업이 완료되었을 때 수행되는 함수입니다. 비동기 작업의 결과를 처리하기 위해 주로 사용됩니다.

## Promise

비동기 작업의 결과를 나타내는 객체입니다. 콜백 지옥 문제를 해결하기 위해 도입되었습니다.
then, catch 매서드를 사용해서 결과와 에러를 처리할 수 있습니다.

- 상태:
  - pending: 작업이 진행 중
  - fulfilled: 작업이 성공적으로 완료
  - rejected: 작업이 실패

## async/await

async는 함수 앞에 붙어 함수가 promise 객체를 반환하도록 지정합니다.
await는 promise가 resolve될 때까지 기다립니다. 값을 할당받아 사용할 수 있습니다.

## 비동기 작업 처리 과정

1. 콜스택에 코드를 실행. 비동기 작업은 백그라운드에서 작업 실행
2. 비동기 작업이 완료되면 콜백(then, catch)이 태스크 큐에 저장됨
   마이크로 태스큐는 promise의 콜백을 저장하고, 매크로 태스크 큐는 setTimeout Web API, DOM 이벤트를 저장.
3. 이벤트 루프는 콜스택이 비어 있는 것을 확인하여 마이크로 테스크 큐부터 시작해서 콜스택으로 이동.
4. 콜스택에서 작업이 실행.
