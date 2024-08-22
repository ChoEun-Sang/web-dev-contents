## DocumentFragment

Dom 변경사항이 발생하면 요소의 위치와 크기를 다시 계산해서 랜더링하는 reflow, repaint 가 발생한다. 변경사항이 발생할 때마다 reflow와 repaint가 발생하면 성능상 좋지 않는다.

DocumentFragment 객체를 사용해서 HTTL 요소를 추가하거나 조작할 수 있는데, 실제 웹 페이지에는 시각적 변화가 나타나지 않는다. reflow와 repaint를 줄일 수 있다.

1. createDocumentFragment 매서드를 사용해서 DOM 요소를 일시적으로 저장하는 객체를 만든다.
2. 객체를 사용해서 DOM 요소를 조작하지만, 실제 DOM에는 영향을 주지 않는다.
3. 여러 개의 요소의 변경사항을 한번에 실제 DOM에 반영한다. 이때, Reflow가 발생하며 다시 DOM를 업데이트하게 된다.

```js
<ul id="list"></ul>;
const ul = document.getElementById("list");
const fragment = document.createDocumentFragment(); // (a)

for (let i = 0; i < 10; i++) {
  const li = document.createElement("li"); // (b)
  li.textContent = `아이템 ${i + 1}`;
  fragment.appendChild(li);
}

ul.appendChild(fragment); // (c)
```

[DocumentFragment 객체로, 성능 좋게 DOM 조작하기](https://mong-blog.tistory.com/entry/DocumentFragment-%EA%B0%9D%EC%B2%B4%EB%A1%9C-%EC%84%B1%EB%8A%A5-%EC%A2%8B%EA%B2%8C-DOM-%EC%A1%B0%EC%9E%91%ED%95%98%EA%B8%B0#google_vignette)
