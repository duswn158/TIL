### javasctipt

------



클로저 함수 : 함수안에 함수

```javascript
// 클로저 : 외부함수 안에 있는 내부함수 (외부 함수에 접근 가능 -> 변수, 파라미터)
// 함수 내부에 함수를 만들어서 함수를 리턴함
// 안쪽에 있는 함수는 그걸 감싸고있는 함수의 값을 사용할 수 있음
	function closureTest(val){
	    var msg = "!!!!!";
	    function addVal(){
	        alert(val + msg);
	    }
	    
	    return addVal;
	}
	
	// closureTest 함수에 글자를 넣고 실행하는 함수를 변수 amEdu에 넣음
	var amEdu = closureTest("Javascript");
	
	// 함수로 값을 받아서 closureTest에 대입하고 실행함
	function pmEdu(val){
		
		// closureTest(val); -> 하면 addVal이 리턴됨
		// var returnVal = closureTest(val); // 리턴받은 함수를
		// returnVal();  //실행함
		// alert(returnVal);
		
		closureTest(val)(); // 위 구문을 단축시킨거나 마찬가지
        // 함수가 값으로 리턴된것이고 리턴된 값을 실행하라 는 뜻.		
	}
```



- Jvascript 에서 함수자체가 '값' 이기 때문에 리턴도되고, 함수안에 함수 사용도됨
- Java에서는 다른 메서드에 있는 변수를 가져오려면 호출해서 객체를 만들어 사용해야 하지만 javascript는 함수안에 함수를 생성하고 안쪽에 있는 함수가 외부 함수의 변수를 사용할 수 있다.



- Javascript에 타입 추론은 모든값이 들어간다. Type Script 는 타입 추론의 단점인 유지보수가 힘들다는것을 보안하기위해 타입추론을 하지말고 Java처럼 지정해서 해야함 이걸 하면 angula 등을 사용 할 수 있음 react, vew가 더 자주 쓰이긴함



javascript에는  **arguments**객체가 만들어져 있는데 해당 함수로 전달된 아규먼트들을 자동으로 배열객체로 만들어서 배열로 저장해주는 객체

- varTest() 에 파라미터를 넣지 않아도 아래 html태그에서 가져오는 값들을 자동으로 집어넣어 저장한다.
- varTest(val1,val2,val3) 으로 3개 받겠다고 지정해 주고 아래에서 값을 동일하개 4개 주어도 이상없이 동작된다
- 무한대로 파라미터 값을 받을 수 있다

```javascript
function varTest(){
		var val = "";
		for (var i = 0; i < arguments.length; i++){
			var += arguments[i] + " ";
		}
		alert(val);
	}
```

```html
<h2 onclick="varTest('kh','정보','교육원','Qclass');">args(arguments)</h2>
```



- 처음 페이지로 들어가 화면이 보이는 상태는 이미 자바스크립트가 처음부터 끝까지 읽어서 객체 저장하고 머하고 다 된 상태.



특정 부분 클릭시 이미지 태그 다른 이미지로 바꾸기

```javascript
var num = 1;
	
function prevGallery(){
	num--;
	if(num < 1){
		num = 7;
	}
	
    // ID gallery를 찾아서 src를 변경
	document.getElementById("gallery").src = "resources/img/img0"+num+".jpg";
	return false; //이벤트 전파 막기 href = 네이버로 가는걸 막아줌
}


function nextGallery(){
	num ++;
	if(num < 1){
		num = 7;
	} else if(num > 7){
		num = 1;
	}
		
	document.getElementById("gallery").src = "resources/img/img0"+num+".jpg";
	//console.log(num);
	return false;
}
```

```html
<div id = "gallerywrap">
		<p>
			<a href="http://www.naver.com" onclick="return prevGallery();">
				<img alt = "이전그림" src = "resources/img/arrowleft.png">
			</a>
			
			<img alt = "갤러리그림" src = "resources/img/img01.jpg" id="gallery">
			
			<a href="#next" onclick="nextGallery();">
				<img alt = "다음그림" src = "resources/img/arrowright.png">
			</a>
		</p>
	</div>
```

