## 이벤트 위임에서 `event.target.matches("button")` vs `closest` 선택하기

이벤트 위임에서 `event.target.matches("button")` 와 `closest` 는 모두 클릭 이벤트 발생 시 타겟 요소가 버튼인지 확인하는 데 사용될 수 있습니다. 하지만 각각의 특징과 사용 시 고려해야 할 점이 다르므로, 어떤 메서드를 선택할지는 상황에 따라 달라집니다.

### `event.target.matches("button")`

- **장점:**
  - **직관적:** 이벤트가 발생한 요소 자체가 버튼인지 여부를 간단하게 확인합니다.
  - **성능:** 일반적으로 `closest`보다 성능이 좋습니다. 특히 많은 자식 요소를 가진 노드에서 더욱 효과적입니다.
- **단점:**
  - **제한적:** 이벤트가 발생한 요소가 반드시 버튼이어야만 합니다. 버튼의 자식 요소에서 이벤트가 발생한 경우에는 확인할 수 없습니다.

### `closest`

- **장점:**
  - **유연성:** 이벤트가 발생한 요소 또는 그 부모 요소 중에서 버튼을 찾을 수 있습니다. 버튼의 자식 요소에서 이벤트가 발생한 경우에도 버튼을 찾을 수 있습니다.
  - **복잡한 선택기 지원:** CSS 선택기를 사용하여 더 복잡한 조건으로 요소를 찾을 수 있습니다.
- **단점:**
  - **성능:** `matches`에 비해 성능이 약간 느릴 수 있습니다. 특히 DOM 트리를 많이 거슬러 올라가야 하는 경우 성능 저하가 발생할 수 있습니다.

### 어떤 것을 선택해야 할까요?

- **이벤트가 발생한 요소가 반드시 버튼이어야 하는 경우:** `event.target.matches("button")`를 사용하면 됩니다.
- **버튼의 자식 요소에서 이벤트가 발생한 경우에도 버튼을 찾아야 하는 경우:** `closest`를 사용해야 합니다.
- **더 복잡한 조건으로 요소를 찾아야 하는 경우:** `closest`를 사용하여 CSS 선택기를 활용할 수 있습니다.
- **성능이 중요한 경우:** `event.target.matches("button")`를 우선적으로 고려할 수 있습니다.

### 예시 코드

```javascript
// event.target.matches("button") 예시
document.querySelector(".container").addEventListener("click", (event) => {
  if (event.target.matches("button")) {
    console.log("버튼 클릭!");
  }
});

// closest 예시
document.querySelector(".container").addEventListener("click", (event) => {
  const button = event.target.closest("button");
  if (button) {
    console.log("버튼 클릭!");
  }
});
```

**결론:**

어떤 메서드를 선택할지는 개발자가 구현하려는 기능과 성능, 유연성 등을 종합적으로 고려하여 결정해야 합니다. 일반적으로 `closest`가 더 유연하고 다양한 상황에 적용할 수 있지만, 성능이 중요한 경우에는 `matches`를 사용하는 것이 좋습니다.

**추가 고려 사항:**

- **브라우저 호환성:** `closest`는 IE11 이하에서는 지원되지 않으므로 폴리필을 사용하거나 다른 방법을 고려해야 합니다.
- **성능 최적화:** 많은 요소를 가진 DOM에서 `closest`를 반복적으로 사용하는 경우 성능 저하가 발생할 수 있으므로, 필요에 따라 성능 최적화 기법을 적용해야 합니다.

**궁금한 점이 있다면 언제든지 질문해주세요.**
