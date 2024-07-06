### npm (Node Package Manager)

`npm`은 Node.js의 기본 패키지 관리자입니다. 패키지 설치, 관리, 스크립트 실행 등을 담당합니다.

#### 주요 기능

1. **패키지 설치**

   - 전역 설치: 시스템 어디서나 사용 가능한 패키지를 설치합니다.

     ```sh
     npm install -g <package-name>
     ```

     예시: `npm install -g typescript` (전역적으로 TypeScript 설치)

   - 로컬 설치: 프로젝트 디렉토리 내에서만 사용 가능한 패키지를 설치합니다.
     ```sh
     npm install <package-name>
     ```
     예시: `npm install express` (현재 프로젝트에 Express 설치)

2. **스크립트 실행**

   - `package.json` 파일에 정의된 스크립트를 실행합니다.
     ```sh
     npm run <script-name>
     ```
     예시: `npm run dev` (package.json 파일에 정의된 dev 스크립트 실행)

3. **패키지 관리**
   - 패키지 업데이트, 제거, 목록 확인 등의 작업을 수행합니다.
     ```sh
     npm update <package-name>
     npm uninstall <package-name>
     npm list
     ```
     예시: `npm update lodash` (Lodash 패키지 업데이트)

### npx (Node Package eXecute)

`npx`는 npm 5.2.0 버전 이후에 포함된 도구로, 패키지를 설치하지 않고 실행할 수 있게 해줍니다. 일회성 명령을 실행하거나, 특정 버전의 패키지를 사용할 때 유용합니다.

#### 주요 기능

1. **일회성 패키지 실행**

   - 패키지를 설치하지 않고, 일회성으로 실행합니다.
     ```sh
     npx <package-name>
     ```
     예시: `npx create-react-app my-app` (React 앱 생성 도구를 설치하지 않고 실행)

2. **특정 버전 패키지 실행**

   - 특정 버전의 패키지를 설치하지 않고 실행합니다.
     ```sh
     npx <package-name>@<version>
     ```
     예시: `npx typescript@3.9.7 --version` (특정 버전의 TypeScript 실행)

3. **프로젝트 로컬 패키지 실행**
   - 프로젝트의 `node_modules`에 설치된 패키지를 실행합니다.
     ```sh
     npx <package-name>
     ```
     예시: `npx jest` (프로젝트에 로컬로 설치된 Jest 실행)

### 예시 상황

#### npm 예시

- **로컬 패키지 설치 및 사용**

  ```sh
  npm install lodash
  ```

  - 프로젝트에서 Lodash 라이브러리를 설치하고, 코드에서 사용합니다.

  ```javascript
  const _ = require("lodash");
  console.log(_.random(1, 100));
  ```

- **스크립트 실행**
  - `package.json` 파일에 정의된 스크립트를 실행합니다.
  ```json
  {
    "scripts": {
      "start": "node server.js",
      "test": "jest"
    }
  }
  ```
  ```sh
  npm run start
  npm run test
  ```

#### npx 예시

- **일회성 패키지 실행**

  ```sh
  npx create-react-app my-app
  ```

  - React 앱 생성 도구를 설치하지 않고, 한 번만 실행하여 새로운 React 앱을 생성합니다.

- **특정 버전 패키지 실행**

  ```sh
  npx typescript@3.9.7 --version
  ```

  - 특정 버전의 TypeScript를 설치하지 않고 실행하여 버전을 확인합니다.

- **프로젝트 로컬 패키지 실행**
  ```sh
  npx jest
  ```
  - 프로젝트의 `node_modules`에 설치된 Jest 테스트 러너를 실행합니다.

요약하자면, `npm`은 주로 패키지 설치, 관리 및 스크립트 실행에 사용되고, `npx`는 일회성 패키지 실행이나 특정 버전 패키지 실행에 유용합니다. `npx`는 설치 과정 없이 필요한 패키지를 바로 실행할 수 있어서 편리합니다.
