## DOM 조작

HTML 코드에서 <li> 태그를 자바스크립트를 이용하여 동적으로 돔을 제어하기 하기

```js
<ul class="list">
  <li>1번</li>
  <li>2번</li>
  <li>3번</li>
</ul>
```

1. querySelectorAll()을 이용하여 가져 온 li 요소들은 NodeList라는 이름의 객체로 반환된다.

```js
const li_list = document.querySelectorAll(".list li");
```

2. querySelector(".list).chlidren으로 li 요소에 접근하면 HTMLCollection으로 반환된다.

```js
const li_list = document.querySelector(".list").chlidren;
```

## NodeList

- Array 형태이지만, 배열과는 다른 유사 배열인 'NodeList'.
- 대부분의 NodeList는 DOM의 변경 사항을 실시간으로 반영한다. (라이브 콜렉션)
- querySelectorAll 매서드에서 반환된 NodeList는 DOM 변경사항이 실시간으로 반영되지 못한다. (정적 콜렉션)

## HTMLCollection

- 유사 배열 형태
- childrent, getElementByClassName, getElementsByTagName 매서드에 의해 반환된다.
- DOM 변경사항을 실시간으로 반연한다. (라이브 콜렉션)

## Live Collection과 Static Collection

NodeList가 Live Collection인지, Static Collection인지 고려하지 않을 경우, 오류가 발생할 수 있다.

.txt-blue 클래스의 색상을 모두 red로 변경하려고 할 때, 실제 색상은 2번을 제외한 텍스트만 변경되는 걸 볼 수 있다.
그 이유는, getElementByClassName 매서드는 실시간으로 DOM 변경사항을 반영하기 때문이다.

for 문을 통해 색상이 변경되자 마자, txt-blue의 NodeList에서 제외되기 때문에,
NodeList 인덱스가 변경되게 된다.

```html
<ul>
  <li className="txt-blue">1번</li>
  <li className="txt-blue">2번</li>
  <li className="txt-blue">3번</li>
</ul>
```

```css
.txt-blue {
  color: blue;
}
.txt-red {
  color: red;
}
```

```js
const li_list = document.getElementByClassName("txt-blue");

for (let i = 0; i < li_list.length; i++) {
  li_listp[i].className = "txt-red";
}
```

- 해결 방안

  1. 마지막 인덱스부터 반복을 시작한다.
     마지막 요소부터 컬렉션에서 제거되더라도 다른 요소에 영향을 미치지 않는다.

  ```js
  const li_list = document.getElementByClassName(".txt-blue");

  for (let i = li_list.length - 1; i >= 0; i--) {
    li_list[i].className = "txt-red";
  }
  ```

  2. 정적 컬렉션으로 반복을 실행한다.
     정적 컬렉션은 실시간으로 변경사항을 반영하지 않기 때문에 의도대로 동작한다.
     반복분이 종로된 후 원래 요소가 그대로 존재하며, 단지 클래스명만 바뀐 상태로 저장된다.

  ```js
  const li_list = document.querySelectorAll(".txt-blue");

  for (let i = 0; i < li_list.length; i++) {
    li_listp[i].className = "txt-red";
  }
  ```

## 참고

[[JS/DOM] 자바스크립트, 돔 조작 시 주의할 점 (Live Collection vs Static Collection)](https://im-developer.tistory.com/110)
