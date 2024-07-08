## `</body>` 태그 직전에 `<script>` 태그를 넣는 이유

웹 페이지 로딩 속도와 사용자 경험을 최적화하기 위해서입니다. 주요 이유와 함께 구체적인 예시는 다음과 같습니다.

1. **페이지 로딩 성능 최적화**:
   `<script>` 태그를 `<head>` 태그 안에 넣으면, 스크립트 로드와 실행이 완료될 때까지 HTML 파싱이 중단됩니다. 이는 페이지 로딩을 지연시킬 수 있습니다. 반면, `<body>` 태그 직전에 스크립트를 넣으면, HTML 문서가 모두 파싱된 후에 스크립트가 로드되고 실행되므로, 페이지 로딩 속도가 빨라집니다.

   ```html
   <body>
     <!-- Page content -->
     <script src="main.js"></script>
   </body>
   ```

2. **DOM 요소 접근 보장**:
   스크립트가 실행되기 전에 DOM(Document Object Model)이 완전히 로드되고 생성되어야 합니다. 그렇지 않으면 스크립트에서 DOM 요소를 찾을 수 없기 때문에 오류가 발생할 수 있습니다. 스크립트를 `</body>` 태그 직전에 배치하면, 스크립트가 실행될 때 DOM이 이미 준비되어 있어 이러한 문제를 방지할 수 있습니다.

   ```html
   <body>
     <!-- Page content -->
     <script>
       document.addEventListener("DOMContentLoaded", function () {
         // DOM 요소 접근 예시
         const button = document.getElementById("myButton");
         button.addEventListener("click", function () {
           alert("Button clicked!");
         });
       });
     </script>
   </body>
   ```

3. **비동기 로드 및 지연 로드**:
   `<script>` 태그에 `async` 또는 `defer` 속성을 추가하면 스크립트 로드를 비동기적으로 처리할 수 있지만, 모든 브라우저가 이를 지원하지 않을 수 있습니다. 스크립트를 `</body>` 태그 직전에 넣으면 기본적으로 HTML 파싱이 완료된 후에 스크립트가 실행되기 때문에 `async`나 `defer` 속성을 사용하지 않더라도 유사한 효과를 얻을 수 있습니다.

   ```html
   <body>
     <!-- Page content -->
     <script src="main.js" defer></script>
   </body>
   ```

이와 같이, `</body>` 태그 직전에 `<script>` 태그를 배치하면 페이지 로딩 성능이 개선되고, 스크립트가 실행될 때 필요한 DOM 요소들이 이미 준비되어 있어 오류를 방지할 수 있습니다. 이는 사용자 경험을 향상시키는 중요한 웹 개발 기법 중 하나입니다.
