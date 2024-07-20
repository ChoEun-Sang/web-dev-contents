## innerHTML를 지양해야 하는 이유

innerHTML는 DOM 요소를 추가하는 JavaScript 매서드이다. string 형식으로 HTML 태그를 사용해서 원하는 요소를 추가할 수 있다. 하지만 성능 측면을 고려했을 때 사용을 지양해야 한다. 그 이유는 innerHTML를 사용하면 코드를 직렬화해서 파싱하는 단계를 거치기 때문에 페이지 로드 속도가 느리다.

innerHTML를 사용하는 대신 insertAdjacentHTML/insertAdjacentElements/insertAdjacentText 를 사용하는 게 좋다. 이 매서드들은 파싱 단계가 없이 DOM Tree에 Node를 insert하기 때문에 innerHTML보다 성능면에서 좋다.

'can i use' 사이트에서 크로스 브라우징 부분에서도 대부분의 브라우저 버전에서 사용이 가능하기 때문에 innerHTML보다 insertAdjacent 를 사용하자.

한가지 더, 문자열만 랜더링하는 경우엔 TextContent > insertAdjacentText > innerHTML 순으로 추천한다.

가급적 innerHTML를 피하는 게 좋다.

- innerHTML과 insertAdjacentHTML 비교

|       매서드       |                      사용 방법                      |                                            비고                                            |
| :----------------: | :-------------------------------------------------: | :----------------------------------------------------------------------------------------: |
|     innerHTML      | document.element.innerHTML = "<div>DOM 변경</div>"; |                                                                                            |
| insertAdjacentHTML |         insertAdjacentHTML(position, text)          | position: beforebegin(앞에), afterbegin(맨앞 child), beforeend(맨뒤 child), afterend(뒤에) |
