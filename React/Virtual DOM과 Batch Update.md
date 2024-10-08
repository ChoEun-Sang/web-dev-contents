## 가상돔 (Virtual DOM)

HTML 파싱해서 DOM 트리를 그립니다.
DOM API를 사용해서 DOM 조작하는데, 레이아웃이나 색상이 바뀌면 리플로우와 리펜인트가 발생합니다.
이때, DOM 전체를 다시 그리는데 많은 비용이 발생합니다.

React는 가상돔을 사용해서 리플로우 리페인트 과정을 최소화하여 성능을 향상시킵니다.
업데이트 되기 전 가상돔을 캡처해서 메모리에 유지하고, 업데이트 된 가상돔과 비교해서(diffing) 변경된 부분만 실제 DOM에 반영합니다. (reconciliation)

이런 방식으로 전체 DOM 트리를 재구축하지 않고, 필요한 부분만 빠르게 업데이트해서 렌더링 성능을 향상됩니다.

## Batch Update

React는 State가 변경되었을 때, 바로 State를 업데이트하여 랜더링하지 않습니다.
변경사항을 적용할 때, 일정 시간 동안 변경사항을 모아서 한번에 적용하는 방식(Batch Update)을 사용해서 리랜더링을 최소화합니다.

그래서 setState는 동기적으로 처리되지 않고, 비동기적으로 처리됩니다. setState가 호출돼도 바로 랜더링이 발생하지 않습니다. setState() 메서드를 사용할 때에는, 배치 업데이트가 일어나는 시점을 고려하여 코드를 작성해야 합니다.

> React 17 및 이전 버전은 브라우저 이벤트에 대한 일괄 처리만 지원합니다. 그러나 React 18 업데이트에서는 자동 배칭이라는 향상된 배칭 버전을 도입했다.
> 이렇게 하면 출처에 관계없이 모든 상태 업데이트에 대한 일괄 처리가 활성화됩니다.

## fluxSync 매서드

만약 setState를 동기적으로 처리해서 바로 랜더링을 하고 싶다면, react-router-dom의 fluxSync 매서드를 사용할 수 있습니다. 하지만, 공식문서에서는 flushSync 사용은 앱 성능에 부정적인 영향을 줄 수 있으니 권장하진 않습니다.

> flushSyncReact가 제공된 콜백 내부의 모든 업데이트를 동기적으로 플러시하도록 강제할 수 있습니다. 이렇게 하면 DOM이 즉시 업데이트됩니다.
>
> ```js
> flushSync(callback);
> ```

React의 렌더링 방식은 컴포넌트 기반의 UI 라이브러리로서, 사용자 인터페이스를 동적으로 업데이트하는 방식을 의미합니다. 이를 이해하기 위해 React의 렌더링 방식, 핵심 개념인 Virtual DOM, 그리고 렌더링이 발생하는 과정에 대해 자세히 설명하겠습니다.

### 1. **React 렌더링의 기본 개념**

React는 애플리케이션의 UI를 구성하는 컴포넌트들이 데이터의 변화를 감지하고 이를 기반으로 UI를 업데이트합니다. UI 변경이 필요한 부분만 업데이트하여 전체 페이지를 다시 그리는 방식보다 효율적입니다.

React의 렌더링은 두 단계로 이루어집니다:

1. **Render Phase (렌더 단계)**: 컴포넌트의 상태나 props가 변경되면 React는 새로운 UI를 만들기 위한 Virtual DOM을 생성합니다.
2. **Commit Phase (커밋 단계)**: 실제 DOM에 변경 사항이 적용되는 단계로, React는 Virtual DOM과 실제 DOM을 비교(Diffing)하고 필요한 부분만 업데이트합니다.

### 2. **Virtual DOM이란?**

Virtual DOM은 React가 렌더링 성능을 높이기 위해 사용하는 추상화된 DOM입니다.

- 실제 DOM을 직접 조작하는 대신, 메모리상에 가상의 DOM을 만들어서 UI의 변경 사항을 관리합니다.
- React는 상태나 props가 변경될 때마다 전체 UI를 Virtual DOM에 렌더링하고, Virtual DOM과 이전 상태의 Virtual DOM을 비교하여 바뀐 부분만 실제 DOM에 반영합니다. 이를 **Diffing 알고리즘**이라고 합니다.

#### **Virtual DOM의 장점**

- 실제 DOM 조작보다 속도가 빠릅니다.
- 전체 DOM을 다시 그리지 않고 변경된 부분만 효율적으로 업데이트할 수 있어 성능이 향상됩니다.

### 3. **렌더링 과정의 흐름**

React의 렌더링 과정은 크게 다음과 같이 이루어집니다:

1. **초기 렌더링 (Initial Render)**

   - 애플리케이션이 처음 로드되면 컴포넌트가 마운트되고, Virtual DOM이 생성된 후 실제 DOM에 적용됩니다.

2. **업데이트 렌더링 (Re-Render)**

   - 상태(State)나 props가 변경되면 React는 해당 변경 사항을 감지하고 렌더링을 다시 수행합니다.
   - 이때 변경된 내용이 Virtual DOM에 반영되고, 이전 Virtual DOM과 비교하여 실제 DOM의 업데이트가 필요한 부분만 효율적으로 업데이트됩니다.

3. **언마운트 (Unmounting)**
   - 컴포넌트가 더 이상 필요하지 않게 되면, React는 이를 실제 DOM에서 제거합니다.

### 4. **렌더링 최적화 기법**

React는 렌더링 과정에서 효율적인 업데이트를 수행하지만, 더 나은 성능을 위해 최적화 기법들을 사용할 수 있습니다:

- **`React.memo`**:
  - 함수형 컴포넌트를 메모이제이션하여 props가 변경되지 않는 경우 재렌더링을 방지합니다.
- **`useMemo`** / **`useCallback`**:

  - `useMemo`: 계산 비용이 큰 연산을 메모이제이션하여 필요할 때만 재계산합니다.
  - `useCallback`: 함수가 재생성되는 것을 방지하여 불필요한 렌더링을 줄입니다.

- **`shouldComponentUpdate`**:

  - 클래스형 컴포넌트에서 컴포넌트가 업데이트될 필요가 있는지 확인하는 메서드입니다.

- **React의 키 프로퍼티 (`key` prop)**:
  - 리스트 렌더링 시 각 아이템에 고유한 `key`를 부여하여 효율적인 업데이트를 가능하게 합니다.

### 5. **CSR, SSR, SSG, ISR과 같은 다양한 렌더링 방식**

React는 다양한 렌더링 방식을 지원합니다:

- **CSR (Client-Side Rendering)**:

  - 초기 로드 시 빈 HTML 파일을 로드하고, 브라우저에서 JavaScript를 실행하여 UI를 렌더링합니다. 초기 로딩 속도는 느리지만, 이후에 빠른 인터랙션이 가능합니다.

- **SSR (Server-Side Rendering)**:

  - 서버에서 렌더링된 HTML을 생성하여 브라우저에 전달합니다. 초기 로딩 속도가 빠르고, SEO에 유리합니다. `Next.js`와 같은 프레임워크를 통해 구현할 수 있습니다.

- **SSG (Static Site Generation)**:

  - 빌드 시점에 HTML을 미리 생성하여 서버에 저장합니다. 정적 파일을 제공하므로 빠른 로딩 속도를 자랑하며, SEO에도 유리합니다.

- **ISR (Incremental Static Regeneration)**:
  - SSG와 SSR의 장점을 결합한 방식으로, 빌드 후에도 페이지의 일부를 주기적으로 갱신할 수 있습니다.

### **결론**

React의 렌더링 방식은 Virtual DOM을 활용하여 효율적으로 UI를 업데이트하며, 다양한 렌더링 방식과 최적화 기법을 제공하여 개발자에게 성능 향상과 유연성을 제공합니다. React의 렌더링 과정과 최적화 방법을 잘 이해하고 활용하면, 보다 효율적인 React 애플리케이션을 구축할 수 있습니다.
