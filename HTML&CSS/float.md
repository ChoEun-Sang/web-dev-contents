## float가 어떻게 작동하는지 설명하세요.

Float는 CSS 위치 지정 속성입니다. Float된 요소는 페이지의 흐름의 일부가 되며, 페이지의 흐름에서 제거되는 position: absolute 요소와 달리 다른 요소(예: 플로팅 요소 주위로 흐르는 텍스트)의 위치에 영향을 줍니다.

CSS clear 속성은 float 요소에 left/right/both에 위치하도록 사용될 수 있습니다.

부모 요소에 float 요소만 있으면, 그 높이는 무효가 됩니다. 컨테이너의 float 요소 다음에 있지만 컨테이너가 닫히기 전에 float를 clear 하면 해결할 수 있습니다.

.clearfix는 영리한 CSS 가상 선택자 (:after)를 사용하여 float를 제거합니다. 상위 클래스에 overflow 를 설정하는 대신 추가 클래스 clearfix를 적용합니다. 그 다음 아래 CSS를 적용하세요:

```css
.clearfix:after {
  content: " ";
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

대신, 부모 요소에 overflow: auto나 overflow: hidden 속성을 주면, 자식 요소 내부에 새로운 블록 포맷 컨텍스트을 설정하고 자식을 포함하도록 확장합니다.

### 참고자료

https://css-tricks.com/all-about-floats/
