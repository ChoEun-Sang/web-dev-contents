## innerHTML를 쓰면 안 되는 이유

### 1. 보안 문제

`innerHTML`을 사용하여 사용자 입력을 처리할 경우, 크로스 사이트 스크립팅(XSS) 공격에 취약해질 수 있습니다. 공격자가 악성 스크립트를 포함한 HTML 코드를 삽입할 수 있으며, 이는 웹 애플리케이션의 보안에 심각한 위협이 됩니다.

예시:

```javascript
const userInput = "<img src='invalid-url' onerror='alert(\"XSS Attack\")'>";
document.getElementById("output").innerHTML = userInput;
```

위 코드는 `innerHTML`을 사용하여 사용자 입력을 그대로 삽입하기 때문에 XSS 공격에 노출됩니다.

### 2. 성능 문제

`innerHTML`을 사용하면 기존 DOM 트리를 재구성해야 하므로 성능 저하가 발생할 수 있습니다. 특히 큰 데이터셋이나 복잡한 DOM 구조를 업데이트할 때 문제가 됩니다.

예시:

```javascript
const newContent = "<div><p>New content</p></div>";
document.getElementById("content").innerHTML = newContent;
```

이 경우, 브라우저는 `content` 요소의 자식 요소들을 모두 제거하고 새롭게 생성된 요소들을 삽입해야 하므로 성능 저하가 발생할 수 있습니다.

### 3. 유지보수성 문제

`innerHTML`은 문자열을 통해 HTML을 삽입하는 방식이므로 코드 가독성이 떨어지고, 디버깅이 어려울 수 있습니다. 특히 복잡한 HTML 구조를 문자열로 작성하면 유지보수가 어려워집니다.

예시:

```javascript
document.getElementById("content").innerHTML =
  "<div class='item'><h2>Title</h2><p>Description</p></div>";
```

이렇게 HTML 코드를 문자열로 작성하면 가독성이 떨어지며, 나중에 수정할 때 오류를 발생시키기 쉽습니다.

### 대안 방법

1. **createElement와 appendChild 사용**

   - JavaScript의 DOM 메서드를 사용하여 요소를 생성하고 추가하는 방식이 더 안전하고 유지보수하기 쉽습니다.

   예시:

   ```javascript
   const newDiv = document.createElement("div");
   const newH2 = document.createElement("h2");
   const newP = document.createElement("p");

   newH2.textContent = "Title";
   newP.textContent = "Description";

   newDiv.classList.add("item");
   newDiv.appendChild(newH2);
   newDiv.appendChild(newP);

   document.getElementById("content").appendChild(newDiv);
   ```

2. **textContent 사용**

   - HTML이 아닌 텍스트만 삽입할 때는 `innerHTML` 대신 `textContent`를 사용하여 XSS 공격을 방지할 수 있습니다.

   예시:

   ```javascript
   const userInput = "Safe Text";
   document.getElementById("output").textContent = userInput;
   ```

3. **insertAdjacentHTML 사용**
   요소(element)의 내용을 변경하는 대신 HTML을 문서(document)에 삽입하려면, insertAdjacentHTML() 메서드를 사용하십시오.

```
element.insertAdjacentHTML(position, text);

```

- position 값:

"beforebegin": 대상 요소 바로 앞에 삽입
"afterbegin": 대상 요소의 첫 번째 자식 요소로 삽입
"beforeend": 대상 요소의 마지막 자식 요소로 삽입
"afterend": 대상 요소 바로 뒤에 삽입

### 결론

`innerHTML`을 사용하는 것은 보안, 성능, 유지보수 측면에서 여러 문제를 일으킬 수 있습니다. 대신, DOM 메서드를 사용하여 요소를 생성하고 추가하는 방법을 사용하는 것이 좋습니다. 이를 통해 코드의 안전성과 효율성을 높일 수 있습니다.
