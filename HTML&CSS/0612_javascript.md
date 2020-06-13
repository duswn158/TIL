**ParentNode.append()** 메서드는 ParentNode의 마지막 자식 뒤에 [Node](https://developer.mozilla.org/ko/docs/Web/API/Node) 객체 또는 [DOMString](https://developer.mozilla.org/ko/docs/Web/API/DOMString) 객체를 삽입한다. [DOMString](https://developer.mozilla.org/ko/docs/Web/API/DOMString) 객체는 [Text](https://developer.mozilla.org/ko/docs/Web/API/Text) 노드처럼 삽입한다.

[Node.appendChild()](https://developer.mozilla.org/ko/docs/Web/API/Node/appendChild)와 다른 점:

- ParentNode.append()는 [DOMString](https://developer.mozilla.org/ko/docs/Web/API/DOMString) 객체도 추가할 수 있다. 한편 Node.appendChild()는 오직 [Node](https://developer.mozilla.org/ko/docs/Web/API/Node) 객체만 허용한다.
- ParentNode.append()는 반환하는 값이 없다. 한편 Node.appendChild()는 추가한 [Node](https://developer.mozilla.org/ko/docs/Web/API/Node) 객체를 반환한다.
- ParentNode.append()는 여러 개 노드와 문자를 추가할 수 있다. 한편 Node.appendChild()는 오직 노드 하나만 추가할 수 있다.
- https://developer.mozilla.org/ko/docs/Web/API/ParentNode/append



------







### JQUERY

------

Javascript library

Java library = *jr



프론트엔드 :

angular.js

vue.js

react.js

이런건 자바스크립트 라이브러리 하고 하지만 거의 프레임워크



-> vanila script = 순수 자바스크립트

-> typescript = 타입 안정성을 고려한 스크립트



제이쿼리 홈페이지

https://jquery.com/ 에서 설치.



[Download the compressed, production jQuery 3.5.1 slim build](https://code.jquery.com/jquery-3.5.1.slim.min.js)

= 공백까지 다 최소화 하며 압축 

크기 : 87.3

jquery-3.5.1.min.js

```html
<script type="text/javascript" src="http://code.jquery.com/jquery-latest.min.js"></script>
```



[Download the uncompressed, development jQuery 3.5.1 slim build](https://code.jquery.com/jquery-3.5.1.slim.js)

= 보기쉽게 해둠

크기 : 280

jquery-3.5.1.js



오른쪽 클락 + 다른이름으로 링크 저장. jquery-3.5.1.min.js파일 저장됨

커스터 마이징 할수 있도록 공백포함된 파일도 제공함



- ##### 로컬에서 불러오는 이유 : 

  ##### 온라인에서 받아오면 최신버전을 항상 받아오는데 그럼 혹시나 메서드 만들어둔게 새버젼에서 바뀌어서 충돌날수도 있기때문에 로컬에 받아두고 그걸 사용함 회사by회사 이기 때문에 참고.



제이쿼리 사용하는 이유나 마찬가지 ->

### Ajax

Call a local script on the server `/api/getWeather` with the query parameter `zipcode=97201` and replace the element `#weather-temp`'s html with the returned text.

```javascript
$.ajax({  url: "/api/getWeather",  data: {    zipcode: 97201  },  success: function( result ) {    $( "#weather-temp" ).html( "<strong>" + result + "</strong> degrees" );  }});
```