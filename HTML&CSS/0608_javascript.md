## DOM : Document Object Model

------

<u>DOM은 중요함.</u>

html 문서(document) 요소 -> javascript object(객체)로 변환 -> 우리가 Node / NodeList 로 사용

```javascript
document.getElementsByTagName("p");	// nodeList (array)
document.getElementsByName("");		

document.getElementById("test"); 	// node (ID는 유일하기때문)
```



HTML문서에 있는 무언가를 javascript가 가져올때는

Document

Object

Model 을 찾기 시작함

- html문서 안에있는 태그 하나하나가 객체가되는것.
- 문서를 객체로 바꿔줌
- 객체화된 태그 하나하나는 Node
- 뭉쳐있는건 NodeList (배열)
- 여러개가 있을 가능성이있는 것들은 전부 NodeList로 가져온다.
- 하나도 없어도 빈 배열로 리턴될것.



Element -> node

```javascript
var doc = document.getElementById("test");
```



Elements -> nodeList (값이 몇개인지 모를때 혹은 여러개일때는 무조건 nodeList로 저장함)

```javascript
var doc = document.getElementsByName("test02");
```



예제)	

```javascript
function searchID(){
		// test라는 id를 가진 document에서 element를 하나 가져올것
		var doc = document.getElementById("test");
		alert(doc + " : " + typeof(doc));
		console.log(doc);
		
		doc.innerHTML = "id로 탐색 완료!";
		doc.style.color = "red";
	}
	
	function searchName(){
		
		var doc = document.getElementsByName("test02"); //nodeList로 리턴됨
		doc[1].value = "name으로 탐색 완료!";
		
	}
	
	function searchTagName(){
		var doc = document.getElementsByTagName("p");
		
		// 배열이기 때문에 그냥 doc.style.color 같은 문장은 사용할 수 없음
		doc[3].innerHTML = "tagName으로 탐색!";
		doc[3].style.color = "blue";
	}
function searchQS(){
	// css 선택자를 통해 가져옴 All이라고 붙어서 전부 가져온다. 즉 NodeList로 가져온다.
		var doc = document.querySelectorAll("#test");
		
		doc[0].innerHTML = "css선택자로 탐색";
	}
```


```html
<p class = "select" onclick="searchQS();">DOM 탐색 메서드</p>
<p id = "test" class="select" onclick="searchID();">1. 엘리먼트의 id로 탐색 : 엘리먼트 하나를 선택 (중복 불가) - 값 하나 반환</p>
<p onclick="searchName();">2. 엘리먼트의 name으로 탐색 : 엘리먼트 여러개 선택 - 값 여러개 (배열) 반환 <br>
	<input type="text" name="test02"><br>
	<input type="text" name="test02"><br>
	<input type="text" name="test02"><br>
</p>
	
	
<p class = "select" onclick="searchTagName();">3. 엘리먼트의 태그이름으로 탐색 : 엘리먼트 여러개 선택 - 값 여러개 (배열) 반환 </p>
```



함수 : 독립적으로 있는애들

메서드 : 어딘가에 종속되어있는애들( 자바에서는 무조건 클래스 아래 있어야하기 때문에 메서드만 존재하는것. )



undifined : 정의되지 않았다 (변수없음)

null : 값이없다. (변수 있음)



**this의 용법 - 나중에 찾아보기**



### object

------

```javascript
function myQclass(){
	
	// this = 이 객체(myQclass)가 가지고 있는 name이라는 변수. 
	this.name = "kh정보 교육원";	// 외부에서 접근 가능
	
	var name2 = "빅데이터 전문가 과정"; // 외부에서 접근 불가
	
	// 자바에서의 getter같은 느낌
	this.getName2 = function(){
		return name2;
	}
	
}

// function 키워드, 파라미터 사라지고 바디만 가짐
// 객체 literal 혹은 literal객체 라고 함
var yourQclass = {
		// {key : value, key : value}의 형태
		name : "kh정보교육원",
		print : function(){
			
			//return name + "빅데이터 전문가 과정!"; // -> 문자만 출력됨
			return yourQclass.name + "빅데이터 전문가 과정!"; // -> 위에 name과 더해져서 문자가 출력됨
			
		}
}

//prototype : 기능을 확장시켜줌
myQclass.prototype.printSubjects = function(){
	alert(this.name + " " + this.getName2() + " : java, db, ui");
}

function objTest(){
	// 자바스크립트도 객체지향처럼 만들 수 있음
	var cls = new myQclass();
	
	//alert(cls.name);
	
	// name2 는 undifined 뜸 지역변수기때문에 찾을수 없음  
	//alert(cls.name2);
	
	//alert(cls.getName2());
	
	
	//alert(yourQclass.name);
	//alert(yourQclass.print());
	
	
	cls.printSubjects();
}
```



```html
<pre>
	객체의 구성
	-메서드 : 기능 정의
	-속성 : 객체 내부 데이터
	-this : 객체 내부의 메서드나 속성을 정의할 때 사용
	-프로토타입 : 객체의 확장
</pre>
	
<button onclick="objTest();">클릭</button>
```





### Number

: javascript에서 기본적으로 제공하는 객체 중 하나 라이브러리 개념

------

```javascript
	function numberObj(){
	var out = document.getElementById("inputTxt");
		
//1. 작성 방법
	var num = 7;				// 리터럴 (값 자체)
	var num02 = new Number(7);	// Number 라는 객체 생성
		
	out.innerHTML = num + "<br>";
	out.innerHTML += num02 + "<br>";
		
//2. NaN (Not a Number)
// = -> 대입 , += -> 추가
	out.innerHTML += "NaN 속성 : " + parseInt("a") + "<br>";	// 출력시 NaN(Not a Number) 즉 숫자가 아니라고 뜸
		
//3. infinity (표현 가능한 값보다 더 큰 수, 무한대.)
	out.innerHTML += "infinity 속성 : " + (Infinity/100) + "<br>"; // 무한대 / 100 = 무한대 즉 Infinity 출력됨		
	out.innerHTML += "infinity 속성 : " + (Number.MAX_VALUE + 0.00001e+308) + "<br>"; // e는 자연로그 e
		
		
//4. 자주 쓰는 함수
		
//1) roFixed() : 실수형의 소수점 자리수를 지정하고 문자열로 반환
		var number01 = 333.34567;
		out.innerHTML += "toFixed : " + number01.toFixed(2) + "<br>"; // 소수점 두번째자리까지 출력됨
		
//2) toString(n) : (n진수 변환하여) 문자열로 반환
		var number02 = 123;
		out.innerHTML += "toString(16) : " + number02.toString(16); // 7b 출력됨
		
	}
	
	function isNum(){
		
		var out = document.getElementById("inputTxt");
		
// 창을 띄워 받은 값을 num에 저장
		var num = prompt("숫자만 입력하세요");		
		
// 만일 입력된 값이 숫자라면, "n은 숫자입니다";
// 아니라면, "n은 숫자가 아닙니다."		
		
// isNaN() : 숫자가 아닌지 긴지 판별. Not a Number 인지 아닌지 판별
		if (!isNaN(num)){
			out.innerHTML = num + "은 숫자입니다";
		} else{
			out.innerHTML = num + "은 숫자가 아닙니다.";
		}
		
		
	}
```



```html
	<pre>
		*javascript에서 기본적으로 제공하는 객체 중 하나
		1. Number 객체
		- 정수와 실수를 다루는 객체
		<button onclick="numberObj();">number 객체!</button>
		-속성 : NaN (숫자가 아닌 값)
			  infinity (범위를 벗어난 값)
		- 그 밖의 예외 속성
		undefined (변수가 정의되지 않음
		null (변수는 있지만 값이 없다)
		<button onclick="isNum();">숫자 판별!</button> 
	</pre>
	
	<p id="inputTxt"></p>
```





### trans_object

: 형 변환

------



```javascript
// 넘어오는 값이 정수면 정수로, 실수면 실수로 바꿔줌.
	function numTest(val){
		
// 아래 html태그에서 input태그로 받는 값은 문자형(String)임. 따라서 그 문자를 Number()함수를 사용해 숫자형으로 변환해주는것.
		var vals = Number(val) + 5;
		alert(vals + " : " + typeof(vals));
	}
	
// 넘어오는 값이 정수형의 문자면 정수로, 실수형의 문자도 정수로 변경
	function intTest(val){
		var vals = parseInt(val) + 5;
		alert(vals + " : " + typeof(vals));
	}
	
	function floatTest(val){
		var vals = parseFloat(val) + 5;
		alert(vals + " : " + typeof(vals));
	}
```



```html
	<h2>1. 숫자형 형 변환 number() 함수</h2>
	<p>정수 or 실수의 문자형을 숫자형으로 반환</p>
	<input type="text" id="num">
	<button onclick="numTest(num.value);">확인</button>
	
	<h2>2. 정수형 형 변환 parseInt() 함수</h2>
	<p>정수 or 실수의 문자형을 정수로 반환</p>
	<input type="text" id="int">
	<button onclick="intTest(int.value);">확인</button>
	
	<h2>3. 실수형 형 변환 parseFloat() 함수</h2>
	<p>실수형태 문자형을 정수로 반환</p>
	<input type="text" id="float">
	<button onclick="floatTest(float.value);">확인</button>
```

