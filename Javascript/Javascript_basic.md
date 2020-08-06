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





- API : 어떤 프로그램이 어떻게 실행되는지 알려주는 조작 장치(Application Programming Interface) "사용설명서"
  사용자가 조작하는 장치는 UI (User Interface)
- 패키지 : 자바의 클래스를 묶어서 정리한 것
  클래스 : 서로 연관된 변수와 메소드를 모아 이름을 붙인 것, "디렉토리"
  변수 : 하나의 값을 저장할 수 있는 메모리 공간
  메소드 : 어떤 일을 처리하는 실행문을 모아 넣은 것

- -패키지
  변수 + 메소드 = 클래스
  클래스 + 클래스 + 클래스 +... = 패키지

- -인스턴스
  클래스 PrintWriter 인스턴스 p1 = new Constructor(생성자)PrintWriter("result1.txt");
  클래스를 복제하는 것이 인스턴스
  인스턴스 쓰는 이유 : 클래스에 직접 입력 시 동작이 많아지면 일일히 쓰는 불편함이 있음.
  반복하는 작업 시 효과적

- -상속
  java.lang.Object 부모 클래스
  java.io.Writer 자식 클래스
  java.io.PrintWriter 자식 클래스

부모 클래스가 가진 변수와 메소드를 물려받아 자기가 원하는 변수를 추가하는 것.
클래스 드래그 후 Open Type Hierarchy 누르면 상속 관계를 볼 수 있음.
Override - 기존에 있는 메소드를 내가 정의한 메소드로 덮어씌우는 것



#### 변수 호이스팅(Variable Hoisting)

모든 변수선언은 호이스트 됩니다. 호이스트란, 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되는 것을 의미합니다. 즉, 변수가 함수내에서 정의되었을 경우 선언이 함수의 최상위로, 함수 바깥에서 정의되었을 경우는 전역 컨텍스트의 최상위로 변경됩니다.

변수의 선언이 초기화나 할당시에 발생하는것이 아니라, 최상위로 호이스트 된다는 것을 명심해야 합니다.

```javascript
function showName() {
     console.log("First Name : " + name);
     var name = "Ford";
     console.log("Last Name : " + name);
}
showName();
// First Name : undefined
// Last Name : Ford
// First Name이 undefined인 이유는 지역변수 name이 호이스트 되었기 때문입니다.

```

이 코드는 자바스크립트 엔진에 의해 다음과 같이 해석됩니다.

```javascript
function showName() {
     var name; // name 변수는 호이스트 되었습니다. 할당은 이후에 발생하기 때문에, 이 시점에 name의 값은 undefined 입니다.
     console.log("First name : " + name); // First Name : undefined
     name = "Ford"; // name에 값이 할당 되었습니다.
     console.log("Last Name : " + name); // Last Name : Ford
}
```



호이스트 되었을때, 함수 선언은 변수선언을 덮어 씁니다.

```javascript
// 다음 두 변수와 함수는 myName으로 이름이 같습니다.
var myName; // string

function myName() {
     console.log("Rich");
}
// 함수 선언은 변수명을 덮어 씁니다.
console.log(typeof myName); // function
```



하지만, 변수에 값이 할당될 경우에는 반대로 변수가 함수선언을 덮어 씁니다.

```javascript
var myName = "Richard";

function myName() {
     console.log("Rich");
}

console.log(typeof myName); //string
```

“strict mode”에서 최초의 선언없이 변수에 값을 할당하려 한다면 오류가 발생합니다. 변수에 값을 할당 하려 할때는 항상 미리 선언하는 습관을 들이는것이 좋습니다.



원래는, onclick 으로 인해 javascript에 이벤트가 전달되고, 

js 이벤트가 실행된 후에 다시 html 고유의 속성

href 속성에 의한 이벤트가 발생되는건데 중간에 막힌것. return false를 해버리기 때문.

```javascript
function prevGallery(){
	num--;
	if(num < 1){
		num = 7;
	}
		
	document.getElementById("gallery").src = "resources/img/img0"+num+".jpg";
	return false; //이벤트 전파 막기 href = 네이버로 가는걸 막아줌
}
```

```html
<a href="http://www.naver.com" onclick="return prevGallery();">
	<img alt = "이전그림" src = "resources/img/arrowleft.png">
</a>
```

