`.json()`, `JSON.parse()`, `JSON.stringify()`는 모두 **JSON(JavaScript Object Notation)**을 다룰 때 사용하는 메서드들이지만, 그 역할과 사용 목적이 다릅니다. 각각을 비교해 설명하겠습니다.

### 1. **`.json()` 메서드**

- **설명**: `.json()`은 `fetch` API나 `Response` 객체를 사용하여 HTTP 응답에서 JSON 데이터를 **JavaScript 객체로 변환**할 때 사용하는 메서드입니다.
- **비동기 메서드**이며 `Promise`를 반환합니다.

#### **사용 예시**:

```javascript
fetch("https://api.example.com/users/1")
  .then((response) => response.json()) // 응답을 JSON 형태로 변환
  .then((data) => {
    console.log(data); // 변환된 JavaScript 객체 사용
  })
  .catch((error) => console.error("Error:", error));
```

위의 코드를 보면 `fetch`로 가져온 데이터가 `response.json()`을 통해 **JavaScript 객체**로 변환되는 것을 볼 수 있습니다.

### 2. **`JSON.parse()` 메서드**

- **설명**: `JSON.parse()`는 **JSON 문자열을 JavaScript 객체로 변환**할 때 사용됩니다.
- 서버에서 받아온 데이터가 문자열 형태로 되어 있을 때, 이를 실제로 사용할 수 있는 JavaScript 객체로 변환하는 것이 목적입니다.

#### **사용 예시**:

```javascript
const jsonString = '{"name": "EunSang", "age": 25}';
const obj = JSON.parse(jsonString);

console.log(obj.name); // "EunSang"
console.log(obj.age); // 25
```

여기서 `JSON.parse()`를 통해 `jsonString`이라는 JSON 형식의 문자열이 **JavaScript 객체**로 변환되었습니다.

### 3. **`JSON.stringify()` 메서드**

- **설명**: `JSON.stringify()`는 **JavaScript 객체를 JSON 문자열로 변환**할 때 사용됩니다.
- 이 메서드는 주로 데이터를 서버에 전송하거나 로컬 스토리지에 저장할 때 사용됩니다. 이러한 경우 JavaScript 객체를 **문자열로 변환**해야 하는데, `JSON.stringify()`가 그 역할을 합니다.

#### **사용 예시**:

```javascript
const obj = { name: "EunSang", age: 25 };
const jsonString = JSON.stringify(obj);

console.log(jsonString); // '{"name":"EunSang","age":25}'
```

위 예시에서는 `obj`라는 JavaScript 객체가 JSON 형식의 문자열로 변환되었습니다.

### **요약 및 비교**

| 메서드             | **역할**                             | **입력 데이터 타입**       | **출력 데이터 타입**       |
| ------------------ | ------------------------------------ | -------------------------- | -------------------------- |
| `.json()`          | HTTP 응답을 JavaScript 객체로 변환   | `Response` 객체            | `Promise`로 감싸진 JS 객체 |
| `JSON.parse()`     | JSON 문자열을 JavaScript 객체로 변환 | JSON 문자열 (`string`)     | JavaScript 객체 (`object`) |
| `JSON.stringify()` | JavaScript 객체를 JSON 문자열로 변환 | JavaScript 객체 (`object`) | JSON 문자열 (`string`)     |

### **실제 활용 사례**

- **`.json()`**: `fetch`를 사용해 서버로부터 데이터를 받아올 때, `response.json()`으로 데이터를 JavaScript 객체로 변환하여 활용.
- **`JSON.parse()`**: 로컬 스토리지에서 가져온 문자열 데이터를 JavaScript 객체로 변환하여 사용.
- **`JSON.stringify()`**: JavaScript 객체를 서버로 전송하거나, 로컬 스토리지에 저장할 때 문자열로 변환.

이렇게 각각의 메서드는 서로 다른 목적을 가지고 있어 상황에 맞게 사용해야 합니다.
