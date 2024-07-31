## CORS 에러: 간단히 알아보기

**CORS**는 **Cross-Origin Resource Sharing**의 약자로, **다른 출처의 자원 공유**를 의미합니다. 즉, 서로 다른 도메인이나 포트에서 실행되는 웹 애플리케이션끼리 자원(데이터, 이미지 등)을 주고받을 때 발생하는 보안 관련 이슈를 해결하기 위한 메커니즘입니다.

### 왜 CORS 에러가 발생할까요?

- **동일 출처 정책 (Same-Origin Policy):** 브라우저는 보안상의 이유로, 동일한 도메인, 프로토콜, 포트에서 온 요청만 허용하는 정책을 가지고 있습니다.
- **다른 출처의 자원 요청:** 서로 다른 도메인의 API를 호출하거나, iframe 등을 통해 다른 사이트의 콘텐츠를 포함하려 할 때 CORS 에러가 발생할 수 있습니다.

### CORS 에러가 발생하면 어떤 일이 일어날까요?

- **브라우저 콘솔에 오류 메시지:** `Access to XMLHttpRequest at 'https://example.com/api' from origin 'https://yourdomain.com' has been blocked by CORS policy`와 같은 메시지가 나타납니다.
- **API 요청 실패:** 서버로부터 데이터를 가져오지 못해 웹 페이지가 제대로 작동하지 않을 수 있습니다.

### CORS 에러를 해결하는 방법

- **서버 설정:**
  - **Access-Control-Allow-Origin:** 허용할 출처를 지정합니다. 모든 출처 허용 시 `*`을 사용할 수 있지만, 보안상 권장되지 않습니다.
  - **Access-Control-Allow-Methods:** 허용할 HTTP 메서드(GET, POST 등)를 지정합니다.
  - **Access-Control-Allow-Headers:** 허용할 헤더를 지정합니다.
- **클라이언트 설정:**
  - **CORS 지원 라이브러리 활용:** Axios, Fetch API 등을 사용하여 CORS 설정을 간편하게 처리할 수 있습니다.
- **프록시 서버 활용:** 클라이언트와 서버 사이에 프록시 서버를 두어 요청을 중계하는 방법도 있습니다.

### 예시: Node.js Express 서버에서 CORS 설정하기

```javascript
const express = require("express");
const cors = require("cors");

const app = express();
const port = 3000;

app.use(
  cors({
    origin: "https://yourdomain.com", // 허용할 출처
  })
);

// ... 다른 라우트 설정 ...

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

### 왜 CORS가 필요한가요?

- **보안 강화:** 허용된 출처만 데이터에 접근할 수 있도록 제한하여, XSS(Cross-Site Scripting) 등의 공격을 방지합니다.
- **API 공개:** 다른 개발자가 자신의 API를 안전하게 사용할 수 있도록 합니다.

### iframe이란?

iframe은 HTML 문서 내에 다른 웹 페이지를 포함시킬 수 있는 요소입니다. 마치 웹 페이지 안에 작은 창을 띄워 놓는 것처럼, 다른 웹 서버에서 호스팅되는 콘텐츠를 현재 페이지에 삽입하여 다양한 기능을 구현하는 데 활용됩니다. 예를 들어, 유튜브 영상을 웹 페이지에 직접 embed 하거나, 다른 사이트의 지도를 가져와 보여주는 등의 기능을 구현할 때 iframe을 사용합니다.

iframe을 사용하여 다른 도메인의 콘텐츠를 불러올 때 CORS 에러 발생할 수 있다.
