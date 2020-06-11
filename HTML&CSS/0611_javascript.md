#### js15_check

- 뭔가 속성들에 값을 줄때는 값이 무엇이든 있으면 자바 스크립트가 true로 봄

  따라서 아래는 전체 선택은 되지만 해제가 되지않음.

```javascript
function allsel(check){
		var chks = document.getElementsByName("chk");
		
		for(var i = 0; i < chks.length; i++){
            chks[i].checked = "test";
            //chks[i].checked = check;
        }
	}
```

```html
<input type="checkbox" name="all" onclick="allsel(this.checked);">전체선택<br>
```



**전체코드 :**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>js15_check.html</title>

<style type="text/css">

	#colorbox{
		width: 320px;
		height : 320px;
		position : relative;
	}	
	
	#red, #green, #blue, #yellow{
		width: 150px;
		height: 150px;
		border: 1px solid black;
		position : absolute;
	}
	
	#green{left : 160px;}
	#blue{top : 160px;}
	#yellow{left : 160px; top : 160px;}

</style>

<script type="text/javascript">
	
	// allsel(this.checked); 엘리먼트가 체크되면 아래 함수에 boolean값 넣어주며 실행
	// for문으로 전체선택 태그에 true값이면 아래 체크박스들도 true로 전체선택.
	function allsel(check){
		var chks = document.getElementsByName("chk");
		
		for(var i = 0; i < chks.length; i++){
            chks[i].checked = check;
        }
		
	}
	
	function sel(){
		var chks = document.getElementsByName("chk");
		
		for(var i = 0; i < chks.length; i++){
			
// chks[i]번지 중에 체크 되어있는것만 아래의 명령 실행 하기 위함.
			if(chks[i].checked){
// chks[i]번지의 value값과 동일한 ID를 가진 Node를 불러와서 백그라운드컬러를 chks[i]번지의 value값으로 변경
                
// value값을 색으로 통일해두지 않으면 박스마다 색을 다르게 줄때 하나하나 지정해주어야 하기때문에 chk의 "value"와 dic의 "id"값을 색 이름으로 통일시킨듯
                
// chks[i].value 자동으로 문자열로 리턴
				document.getElementById(chks[i].value).style.backgroundColor=chks[i].value;
			} else{
// check된거 아니면 다시 흰색으로 돌림
				document.getElementById(chks[i].value).style.backgroundColor="";
			}
		}
		
	}
	
	function clearDiv(){
		
// 아이디 colorbox 자식 div태그 전부 선택해서 NodeList로 가져오고
// for문으로 배경색 초기화. ""대신 white 혹은 #ffffff도 가능
// 위에 allsel 함수가 이미 있으니 거기에 false값 집어넣어서 전체 체크박스 체크해제,
// all 체크박스도 가져와서 false로 체크해제
		var colorbox = document.querySelectorAll("#colorbox > div");
				
		for(var i = 0; i < colorbox.length; i++){			
			colorbox[i].style.backgroundColor = "";			
		}
		
		document.getElementsByName("all")[0].checked=false;
		allsel(false);
		
	}

</script>

</head>
<body>

	<div id="colorbox">
		<div id = "red">red</div>
		<div id = "green">green</div>
		<div id = "blue">blue</div>
		<div id = "yellow">yellow</div>		
	</div>
	
	<div id = "base">
		<form>
			<input type="checkbox" name="all" onclick="allsel(this.checked);">전체선택<br>
			
			<input type="checkbox" name="chk" value="red">빨강<br>
			<input type="checkbox" name="chk" value="green">초록<br>
			<input type="checkbox" name="chk" value="blue">파랑<br>
			<input type="checkbox" name="chk" value="yellow">노랑<br>
			
			<input type="button" value="선택" onclick="sel();">
			<input type="button" value="초기화" onclick="clearDiv();">
		</form>
	
	</div>
	
</body>
</html>
```





 체크박스 빨강 해제하면 나머지도 체크해제되도록. 해보기.

```

```



------



#### js16_select



- selectedIndex : 선택한 option 태그의 인덱스를 반환
- options : select 태그의 option'들' 을 반환
- selected : 옵션 선택 여부 (true 혹은 false)



```javascript
function show01(){
		
		var food = document.getElementsByName("food")[0];
		var idx = food.selectedIndex;
		var foodVal = food.options[idx].value;
		
		alert(foodVal + " 먹고싶다...");
		
	} 
	

	function show02(){
		var food = document.getElementsByName("food")[1];
		var sel = "";
		for (var i = 0; i < food.options.length; i++){
			
			if(food.options[i].selected){
				sel += food.options[i].value + ", ";
			}
			
		}
		
		alert(sel + "먹고싶다...");
		
	}
```



- multiple : 여러가지 옵션 한번에 보이며 중복선택하는 옵션창 만듬 파일선택 태그에서 이 속성을 쓰면 파일 다중선택 가능.

```html
<h1>음식 선택하기</h1>
	
	<form>
		<!-- onchange : 무언가 바뀌엇을때 함수실행  -->
		<select name="food" onchange="show01();">
			<option>----------선택-----------</option>
			<option value="치킨">치킨</option>
			<option value="소고기">소고기</option>
			<option value="떡볶이">떡볶이</option>
			<option value="햄버그">햄버그</option>
			<option value="회">회</option>
			<option value="양고기">양고기</option>
			<option value="짜장면">짜장면</option>
		</select>
		
		<br><br><br><br><br><br>
		
		<select name = "food" multiple="multiple" size="7">
			<option value="치킨">치킨</option>
			<option value="소고기">소고기</option>
			<option value="떡볶이">떡볶이</option>
			<option value="햄버그">햄버그</option>
			<option value="회">회</option>
			<option value="양고기">양고기</option>
			<option value="짜장면">짜장면</option>
		</select>
		<button onclick="show02();">선택</button>
	</form>
```



------



### js17_dom01



아래를 alert(divChi.length); 로 찍었을때는 3개.

```html
<div><p>child01</p><p>child02</p><p>child03</p></div>
```



아래는 alert(divChi.length);  가 7개. div와 p태그 사이의 공백 엔터키가 Note로 잡혀서 #text로 잡힘

```html
	<div>
		<p>child01</p>
		<p>child02</p>
		<p>child03</p>
	</div>
```



- 부모태그와 자식태그 찾기 1)  :

```javascript
function test01(){
		
		var p = document.getElementsByTagName("p")[3];
		var parent = p.parentNode;
		
		parent.style.backgroundColor = "yellowgreen";
		
	}
	
	function test02(){
		
		var div = document.getElementsByTagName("div")[2];
		var child = div.childNodes[3];
		
		child.style.fontSize = "20pt";
		
	}
```



```html
<h3 onclick="test01();">1. "test01"태그를 포함한 div태그 의 배경색을 원하는 색으로 적용</h3>
	<h3 onclick="test02();">2. 마지막 div 태그에 포함된 test04 태그의  폰트 크기를 20pt로 적용</h3>

	<div>
		<p>test01</p>
		<p>test02</p>
	</div>
	<div>
		<p>test03</p>
		<p>test04</p>
	</div>
```



- 부모태그와 자식태그 찾기 2) :

```javascript
function searchPar(){
		
		var child02 = document.getElementsByTagName("p")[1];
		// p태그 NodeList [1]번지 태그의 부모 가져옴
		var div = child02.parentNode;
		
		// .nodeName : html태그 이름을 알려줌 대문자로.
		alert(div.nodeName);
		div.style.backgroundColor="green";
		
	}
	
	function searchChi(){
		var div = document.getElementsByTagName("div")[0];
		
		var divChi = div.childNodes;		// NodeList 배열형태 리턴
		
		//alert(divChi.length);
		//alert(divChi[1]);		// [object HTMLParagraphElement] 뜸
		
		// div와 p태그 사이의 텍스트(공백) 까지 Node로 잡히기 때문에 5번지가 되야함.
        // child03을 감싸고있는 p태그의 배경색 변경
		divChi[5].style.backgroundColor = "skyblue"; 
		
		// 아래는 태그들만 가져온것이기 때문에 텍스트까지 배열로 잡히지 않음
		var child03 = document.getElementsByTagName("p")[2];
		child03.style.backgroundColor = "skyblue";
		
	}
```



```html
<h1>부모탐색, 자식탐색</h1>
	
	<div>
		<p>child01</p>
		<p>child02</p>
		<p>child03</p>
	</div>
	
	<button onclick="searchPar();">부모탐색</button>
	<button onclick="searchChi();">자식탐색</button>
```



------



#### <이벤트 발생시 특정 속성가진 태그 생성>

- 엘리먼트 객체 생성하기 : createElement("태그이름");
- text 객체 생성하기 : createTextNode("Text");
- 객체 속성 생성하기 : createAttribute("AttributeName");
- 속성 추가  : setAttributeNode(Attribute);
  		 			 setAttribute("AttributeName", "value"); 



- #####  appendChild : 요소 하위의 요소로 추가. 내 자식요소로 만듬



```javascript
function eleCreate(){
		// 버튼 누를때마다 태그 생성해서 append 하고시픈거.
		
		var div = document.createElement("div");
		// <div></div> 까지 만들어지는것임
		
		/*
		// 속성주는법 1. 
		var attr = document.createAttribute("style");
		// style = ""
		
		attr.nodeValue = "border : 2px solid blue";
		// style = "border : 2px solid blue"; 가 된것
		
		div.setAttributeNode(attr);	// 태그에 속성 넣어줌
		// <div style = "border : 2px solid blue"></div> 가 완성
		*/
		
		// 속성주는법 2.
		div.setAttribute("style", "border : 2px solid red");
		// <div style = "border : 2px solid red"></div> 된것임
	
 		var text = document.createTextNode("생성된 div element");
		// "생성된 div element" 라는 값 하나가 만들어짐
		
		// HTML 하위 요소로 넣어줌
		div.appendChild(text);
		// <div style = "border : 2px solid blue">생성된 div element</div>
		
		document.body.appendChild(div);
		// appendChild : 요소 하위의 요소로 추가. 내 자식요소로 만듬
 }
```



```html
<!-- 중요중요중요 -->

<button onclick="eleCreate();">엘리먼트 생성하기</button>
```



##### 위를 응용해서 이미지 바꿔주는 버튼 만듬  :

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>js20_dom04</title>

<style type="text/css">
	
	img{
		vertical-align : middle;
		width : 300px;
		height : 300px;
	}
	a{
		font-size : 50pt;
		text-decoration : none;
	}

</style>

<script type="text/javascript">

	onload = function(){
		
		var anchs = document.querySelectorAll("a");
		var img = document.querySelector("img");
		var count = 1;
		
		// 왼쪽 a 태그 클릭
		anchs[0].onclick = function(){
			var imgAlt = img.getAttribute("alt");
			
			// 이미지가 첫뻔째 이미지 일때 이전버튼 또누르면 마지막 이미지로
			if (imgAlt == "img01"){
				
				// 카운트 마지막으로 돌려쥬고
				count = 7;
				
				// img태그 src 마지막 사진으로 넘겨쥬공
				img.setAttribute("alt","img07");
				img.setAttribute("src", "resources/img/img07.jpg");
				
			} else { // 위가 아니면 count 하나씩 빼가며 이전 이미지로 넘겨쥼
				img.setAttribute("alt","img0"+(--count));
				img.setAttribute("src","resources/img/img0"+count+".jpg");
			}
		}
		
		// 오른쪽 클릭
		anchs[1].onclick = function(){
			var imgAlt = img.getAttribute("alt");
			
			if (imgAlt == "img07"){
				
				count = 1;
				img.setAttribute("alt","img01");
				img.setAttribute("src", "resources/img/img01.jpg");
				
			} else { // 위가 아니면 count 하나씩 빼가며 이전 이미지로 넘겨쥼
				img.setAttribute("alt","img0"+(++count));
				img.setAttribute("src","resources/img/img0"+count+".jpg");
			}
			
		}
		
	}

</script>

</head>
<body>

	<div>
		<a href="#" id = "lt">◀</a>
		<img alt = "img01" src = "resources/img/img01.jpg">
		<a href = "#" id = "rt">▶</a>
	</div>

</body>
</html>
```



------



#### **children: 자식 요소에 접근** 

현재 요소의 자식 요소가 포함된 HTMLCollection을 반환합니다. 비 요소 노드는 모두 제외됩니다.

![](G:\Text-memo\39일차_children.png)





#### **childNodes: 자식 노드에 접근** (all)

현재 요소의 자식 노드가 포함된 NodeList를 반환합니다. 이때 반환되는 NodeList에는 요소 노드뿐만 아니라 주석 노드와 같은 비 요소 노드를 포함합니다. 

![](G:\Text-memo\39일차_childNodes.png)

요소 노드 이외의 노드가 필요하지 않은 경우라면 children 프로퍼티를 사용하면 되겠습니다.