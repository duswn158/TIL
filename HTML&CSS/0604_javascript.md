### javasctipt

------

react.js

vue.js

angular.js -> typescript



node.js(express.js)



on이라고 붙이면 어떠한 이벤트가 발생하는 자바스크립트.

```
alert('내용'); -> 경고창(메시지팝업)을 발생시키는 명령어
```



function 함수이름 (파라미터){ } 로 사용한다.

함수 이름이 없으면 익명함수 라고 한다.

window.onload -> 윈도우가 로딩된 후



변수 선언 규칙

1. 대소문자 구분
2. 영문,$,_로 시작 그외는 안됨
3. 영문,$,_,숫자 를 포함할 수 있다
4. 키워드나 예약어를 사용 할 수 없다



변수 범위

1. 전역변수 : window 객체에 포함되는 변수. 다른 함수들에서 공용으로 사용할 수 잇다. (값이 유지됨)
2. 지역변수 : 함수나 객체 내부에 선언되고 실행이 종료되면 사라짐



변수 선언 및 저장

1. var 키워드를 사용하여 변수 선언
2. 변수의 타입은 저장되는 타입에 따라 결정된다 (타입추론 : 들어오는 타입을 추론해서 적용해줌)
   - null 값은 object형태로 들어가게됨 값은없는데 타입만 object로 잡는다.
   - **javascript에서는 function = 값 즉, 함수도 값이다.**(변수에 함수가 대입될수 있음)





함수 만들기 기본사항

- 함수를 만들 때는 가급적 크키를 줄이고, 한가지 일을 전문적으로 수행하며, 일반적인 형태로 만드는 것이 좋다. 그래야 함수를 재사용시 용이하다.

- 함수 이름이 변수 이름과 같아지면, 함수 몸체가 바로 값 자체라는 의미이다.

  

1. 문자 (String)

2. 숫자 (number)

 	3. 논리 (boolean)
 	4. null
 	5. 객체(object)
 	6. 함수(function)



javascript 변수의 호이스팅

- **사전적 정의** : 끌어 올리기
- **JavaScript에서의 Hoisting** : 변수의 정의가 그 범위에 따라 **선언과 할당으로 분리되는 것을 의미**한다. 즉, 변수가 함수 내에서 정의되었을 경우, 선언부분만 함수의 최상위로, 함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경이 된다.

https://developer.mozilla.org/ko/docs/Glossary/Hoisting



둘은 다름 그냥 alert()를 쓰면 명령어, 이름을주면 그 함수를 호출하라 가 됨.

```html
<button onclick="alertTest()">클릭!</button>

<button onclick="alert()">클릭!</button>
```



클릭시 창을 띄움

```javascript
// alert : 경고, 코드 디버깅, 단순 출력
	function alertTest(){
		alert("단순대화창 내용 출력");
	}
	
// confirm : 확인/취소 버튼을 제공 각각(true/false)가 리턴됨
	function confirmTest(){
		if(confirm("배경을 파랑으로 변환?")){
			document.body.style.backgroundColor = "skyblue";
		} else {
			document.body.style.backgroundColor="white";
		}
	}

// prompt() : 텍스트 박스 제공, 확인/취소 버튼 제공 -> 확인 버튼 : 텍스트 / 취소 : null값 리턴
	function promptTest(){
		var txt = prompt("좋아하는 과목을 선택해 주세요\n[1:자바, 2:db, 3:web]");
		
		switch(txt){
		case "1":
			alert("역시 자바@");
			break;
		case "2":
			alert("db좋죠");
			break;
		case "3":
			alert("홈페이지 만들기 재밌죠");
			break;
		case null :
			alert("다싫은거니");
			break;
		default :
			alert("1,2,3번 중에 하나만 선택");
		}
		
	}
```



```javascript
// 명시적 함수
	function func01(){
		alert("명시적 함수!!");
	}
	
// 익명 함수 (변수에 함수를 담음, 리터럴 함수에 포함된다고 생각해도 얼추 비슷함)
	var func02 = function(){
		alert("익명 함수!!");
	}
	
	
// 리터럴 함수 (함수를 값으로 사용하는 커다란 개념)
    
	function myLiteralPrn(literal){
		literal("안녕하세요 함수입니다");
	}
	function func03(){
		// 파라미터 하나 받을수 있는 익명함수를 넣은것. 바로 위에있는 myLiteralPrn함수를 \			호출하며 해당 함수에 함수값을 넣어주는것
        // myLiteralPrn(10)이런식으로 주던것이 바뀐거.
        // 함수에서 나온 값이 myLiteralPrn함수로 들어감
        // 그냥 상위 함수에 전달되는 값이 함수타입이라고...
        // 위에 "안녕하세요 함수입니다" + msg 인것임
        // 위 literal 변수에 아래 함수가 들어가서 실행되는것임.
        
		myLiteralPrn(function(msg){
			alert(msg);
		});
        
	}
```



익명함수 :

- 자바스크립트 엔진이 동적으로 생성한다. 따라서 매번 함수가 호출될 때마다 동적으로 생성된다. 예를 들어 반복문 내에서 사용하면 반복될 때마다 생성된다고 보면 된다.



리터럴 함수 :

- ##### 함수는 단지 데이터일 뿐이다.

  - 다른 구문의 식 안에서 함수를 사용하면 함수 리터럴 이다.
  - 함수 리터럴은 함수 이름을 명시하지 않는 것을 제외하고 일반적인 정의모양과 동일하다
  - 값으로 함수를 사용한것
  - 특정 함수명을 갖지 않아도 된다는 점에서는 '익명함수'를 닮았다.
  - 익명함수와는 달리 한번만 파싱된다.
  - 함수가 변수에 배정된다는 사실로 보면 선언함수를 닮았다



![](G:\Text-memo\35일차_javascript_리터럴함수부분.png)