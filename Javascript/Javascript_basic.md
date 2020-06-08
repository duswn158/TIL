### Javascript Basic

------



- Javascript 는 웹브라우저 위에서 동작하는 언어이다.
- 웹브라우저는 웹브라우저 위에서 일어나는 여러가지 사건들 중에  기념할만한 것들 몇가지 약 10 ~ 20가지의 이벤트들을 정의 해두고있음 



##### Event : 기념할만한, 사용자들에게 유용할만한 이벤트들

- onclick : 클릭시 이벤트 발생

- onchange : 내용이 변했을때 이벤트 발생 (한번 실행된 이벤트는 중복 실행되지 않음 ABC로 값이 바뀐 뒤 에는 다른걸 적고 다시 ABC가 된 뒤에 input text 박스에서 마우스가 나가도 이벤트 발생하지 않음)

- onkeydown : 키를 누르면 이벤트 발생

  ```html
  <input type = "button" value="hi" onclick = "alert('hi')">
  <input type = "text" onchange = "alert('changed')">
  <input type = "text" onkeydown = "alert('key down!')">
  ```

  

##### Console : 간단한 계산, 연산을 console창에서 해볼 수 있음

-  텍스트를 긁어서 ''를 붙여 문자로 감싼뒤에 alert(' '.length) 하면 문자가 몇개인지 세어줌
- console에서 실행하는 자바스크립트는 해당 웹페이지에 기반해서 작동됨
- 개발자 창(F12) -> Elements 탭 에서 esc키를 누르면 콘솔창과 함께 볼수 있음
- 랜덤 추출 스크립트 코드 등을 console창에 붙여넣고, 이미 만들어져있는 웹페이지 데이터(태그, 텍스트들, 댓글들 등)를 가져와 코드를 실행 해볼 수있음 (한번 실행 한 코드는 위쪽 화살표 키로 재사용 가능)
- 자바스크립트를 이용한다는 것에는 이미 만들어져있는 웹페이지를 간단한 코드를 작성해 나에게 맞도록 이용할 수 있다는 부분 도 있다.

