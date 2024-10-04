## html 에서 data attribute를 사용하는 이유

HTML에서 `data` attribute를 사용하는 이유는 주로 **비표준** 데이터를 요소에 저장하고 이를 **JavaScript**에서 쉽게 접근하거나 조작하기 위해서입니다. 구체적으로, `data-*` 속성은 다음과 같은 경우에 유용합니다:

1. **비표준 데이터 저장**: HTML에서 기본적으로 제공하지 않는 추가적인 정보를 HTML 요소에 포함시킬 수 있습니다. 예를 들어, 제품 ID, 사용자 상태, 서버에서 가져온 데이터 등을 HTML 요소에 저장할 수 있습니다.

   ```html
   <div data-product-id="12345" data-user-status="active"></div>
   ```

2. **JavaScript에서 쉽게 접근**: JavaScript에서는 `dataset` 속성을 통해 `data-*` 속성에 접근할 수 있습니다. 이를 통해 DOM 요소에 저장된 데이터를 쉽게 가져오거나 변경할 수 있습니다.

   ```javascript
   const productElement = document.querySelector("div");
   console.log(productElement.dataset.productId); // "12345"
   ```

3. **CSS와의 통합**: `data` 속성은 CSS와도 연동할 수 있어서, 특정 상태나 조건에 따라 스타일을 동적으로 적용할 수 있습니다.

   ```css
   div[data-user-status="active"] {
     background-color: green;
   }
   ```

4. **구조적 제약 없음**: `data-*` 속성은 HTML 표준을 따르면서도, 사용자가 필요에 따라 임의의 데이터 속성을 추가할 수 있어 구조적인 제약이 적습니다.

이러한 이유로 `data-*` 속성은 HTML 요소에 데이터를 저장하고, 이를 동적으로 제어할 필요가 있을 때 자주 사용됩니다.
