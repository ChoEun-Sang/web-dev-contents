## `<head>` 태그 안에 `<link>` 태그를 넣는 이유

주로 외부 리소스를 HTML 문서에 연결하기 위해서입니다. 다음은 주요 이유와 함께 구체적인 예시입니다.

1. **CSS 파일 연결**:
   웹 페이지의 스타일을 지정하기 위해 외부 CSS 파일을 링크합니다. 이는 HTML 문서와 스타일을 분리하여 코드의 유지보수성을 높이고, 여러 HTML 문서에서 동일한 스타일을 쉽게 적용할 수 있게 합니다.

   ```html
   <head>
     <link rel="stylesheet" href="styles.css" />
   </head>
   ```

2. **아이콘 설정**:
   웹사이트의 파비콘(favicon)이나 애플 터치 아이콘(Apple Touch Icon) 등을 설정하기 위해 사용합니다. 파비콘은 브라우저 탭에 표시되는 작은 아이콘이고, 애플 터치 아이콘은 모바일 기기 홈 화면에 추가할 때 사용하는 아이콘입니다.

   ```html
   <head>
     <link rel="icon" href="favicon.ico" type="image/x-icon" />
     <link rel="apple-touch-icon" href="apple-touch-icon.png" />
   </head>
   ```

3. **웹 폰트 로드**:
   웹 페이지에서 사용할 외부 폰트를 로드하기 위해 `<link>` 태그를 사용합니다. 예를 들어, Google Fonts에서 폰트를 가져올 때 사용됩니다.

   ```html
   <head>
     <link
       rel="stylesheet"
       href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap"
     />
   </head>
   ```

4. **프리로드 및 프리페치**:
   성능 최적화를 위해 특정 리소스를 미리 로드(preload)하거나 프리페치(prefetch)할 때 사용됩니다. 이는 브라우저가 페이지 로딩 시 더 빠르게 리소스를 가져올 수 있게 도와줍니다.

   ```html
   <head>
     <link rel="preload" href="main.js" as="script" />
     <link rel="prefetch" href="next-page.html" />
   </head>
   ```

5. **캐시 제어**:
   `rel="dns-prefetch"`와 같은 속성을 사용하여 특정 도메인의 DNS 조회를 미리 수행할 수 있습니다. 이는 페이지 로딩 시간을 단축시키는 데 도움이 됩니다.

   ```html
   <head>
     <link rel="dns-prefetch" href="//example.com" />
   </head>
   ```

이처럼 `<link>` 태그는 외부 리소스를 HTML 문서에 연결하거나 페이지 성능을 최적화하는 데 중요한 역할을 합니다. 이를 통해 웹 페이지의 스타일, 아이콘, 폰트 등을 효율적으로 관리하고, 사용자 경험을 향상시킬 수 있습니다.
