### Javascript (array)

------



- 배열은 오브젝트 타입이다.
- 배열은 오브젝트 타입 '객체'이며 prototype으로 구성되어있다



![38일차_javascript_array](G:\Text-memo\38일차_javascript_array.png)



```javascript
var arrayObj = new Array(); 		// 객체 선언
	var arrayObj01 = ["v1","v2", 3, 4];	// 값 넣어서 바로 생선(초기화)
	
	var arrayObj02 = new Array(); 		// 객체 선언
	var arrayObj03 = new Array(5); 		// 객체의 크기(길이)를 정의하며 선언
	
	var arrayObj04 = new Array(1,2,3,4,5);  // 초기화 하면서 객체 생성.
	
	/*
	onload = function(){
		alert(arrayObj04 + " : " + typeof(arrayObj04));
	}
	*/
```



**자바스크립트의 배열 :**

```javascript
function multiArr(){
		var arrLen = 3;
		var arr = new Array(arrLen);
		
		// 2차원 배열
		for(var i = 0; i < arr.length; i++){
			arr[i] = new Array(arrLen);
		}
		
		arr[0][0] = "수박";
		arr[0][1] = "바나나";
		arr[0][2] = "키위";
		
		arr[1][0] = 1;
		arr[1][1] = 2;
		arr[1][2] = 3;
		
		arr[2][0] = ["test","js"];
		arr[2][1] = ["javascript","jquery"];
		arr[2][2] = ["jsp/servelet",["a","b","c"]];
		
		//alert("배열전체 : " + arr.toString());
		// 배열 안에있는 숫자 3 출력
		alert(arr[1][2]);
		
		// 배열 안에있는 "javascript" 출력
		// 2번지의 1번지 안에있는 배열의 0번지 보면 배열 넣었음
		alert(arr[2][1][0]);
		
		// 배열 안에있는 "a" 출력
		alert(arr[2][2][1][0]);
		
	}
```



**배열 연습 HTML 구문 :**

```html
<h1>배열객체</h1>
	
	<ul>
		<li onclick="multiArr();">다중 배열</li>
		<li onclick = "joinTest();">join함수</li>
		<li>배열 정렬			
			<ul>
				<li onclick="sortTest01();">sort() : 문자 정렬</li>
				<li onclick="sortTest02();">sort() : 숫자 정렬</li>
				<li onclick="reverseTest();">reverse() : 반대로 정렬</li>			
			</ul>		
		</li>
		<li onclick="pushAndPop();">배열 저장 방식
			<ul>
				<li>push()</li>
				<li>shift()</li>
				<li>pop()</li>			
			</ul>
		</li>
		<li onclick = "sliceTest();">slice() : 배열의 부분을 가지고 새로운 배열 생성</li>
	</ul>
```



```javascript
function joinTest(){
		var fruitArr = ["사과","포토","수박","망고","딸기"];
		// 요소 하나하나에 "-" 붙여줌
		var res = fruitArr.join("-");
		alert(res);
		
		// 조인으로 배열 값 안에 + 를 붙이고 eval이 그걸 잡아서 배열 전체를 더함
		// 배열 값 자체가 변하는건 아님
		var numArr = [1,2,3,4,5];
		var result = eval(numArr.join("+"));
		alert(result);
	}
```



```javascript
function sortTest01(){
		var arr = ["d","b","a","c","e"];
		alert(arr);
		
		// 정렬 후 출력
		arr.sort();
		alert(arr);
	}
```



```javascript
function sortTest02(){
		var arr = [11, 5, 22, 13, 1, 3, 2, 4, 5];
		alert(arr);
		
		// 아스키 코드 순으로 정렬함 1,11,13 ...
		// arr.sort();
		
		// 함수 사용해서 순서대로 정렬.
		// 양수일때 0일때 음수일때  return받던 comparable과 같음
		// sort 안에 함수가 값 계산해서 리턴 
		// sort가 앞뒤로 배치시킴
		arr.sort(compareNum);
		alert(arr);
		
		// 큰 숫자부터 출력
		arr.sort(function(a,b){
			return b-a;
		})
		alert(arr);
	}

	// 양수일때 0일때 음수일때  return받던 comparable과 같음
	// 뺏을때 양수가 나오는지 음수가 나오는지.
	// A<B 인 경우는 음수를 리턴하고, A=B일 때는 0을 리턴하고, A>B일 때 양수를 리턴한다.
	function compareNum(a,b){
		return a-b;
	}
```



```javascript
function reverseTest(){
		var arr = [11, 5, 22, 13, 1, 3, 2, 5, 4];
		alert(arr);
		
		// 정렬과 상관없이 반대로 출력
		arr.reverse();
		alert(arr);
		
		// sort와 함수로 정렬후 reverse하면 반대로 정렬 출력
		arr.sort(compareNum);
		arr.reverse();
		alert(arr);
	}
```



```javascript
function pushAndPop(){
		var queue = new Array();
		
		// 인덱스에 관계 없이 값 추가
		// 번지수 표기하지않고 그냥 push 순서대로 그냥 들어감
		// 배열이 동적으로 크기가 바뀌며 값이 들어감
		// 자바의 list에 add와 비슷함
		// 자바스크립트의 배열은 자바의 배열과 다르게 동적임.
		queue.push("first");
		queue.push("second");
		queue.push("third");
		alert(queue);
		
		// 배열의 앞에서 값 잘라내기
		// 나간애들은 다시 돌아오지 못함 집나가는거임
		// 배열 사이즈도 줄어들음
		var a = queue.shift(); // first 잘려나옴
		alert(a);
		alert("남은거 : "+queue);
					
		// 배열의 뒤에서 값 잘라내기
		// second만 남음
		var b = queue.pop();
		alert(b);
		alert("남은거 : "+queue);
		
		// 인덱스 상관없이 뒤로 들어감
		queue.push(a);
		queue.push(b);
		alert(queue);
		
	}
```



```javascript
function sliceTest(){
		var arrayOriginal = new Array(1,2,3,4,5,6,7,8,9,10);
		
		// 1번지부터 3번지까지 잘라옴
		// 2,3 두개 잘라옴
		var array01 = arrayOriginal.slice(1,3);
		alert(array01);
		
		var arrayMulti = new Array(4);
		arrayMulti[0] = new Array(1, 2);
		arrayMulti[1] = new Array(3, 4);
		arrayMulti[2] = new Array(5, 6);
		arrayMulti[3] = new Array(7, 8);
		
		// (3,4) (5,6) 뜯어와서 2차원 배열 array02 생성
		// 참조. shallow카피 같은것. 값 수정시 arraymulti 값도 수정.
		var array02 = arrayMulti.slice(1,3);
		alert(array02);
		array02[0][0] = 15;
		alert(array02);
		alert(arrayMulti);
		
		// 4칸짜리를 만들고 5번째 칸을 생성해서 값을 넣어주어도 들어감 즉, 동적임.
		arrayMulti[4] = new Array(9, 10);
		alert(arrayMulti);
		
	}
```



- 클라이언트가 서버한테 다시 요청하는것이 새로고침 즉 reload

```javascript
function locTest(){
    
	//새로고침
	location.reload();
    
	// 네이버로 페이지 이동	
    location.href = "http://www.naver.com";		
	
    // 구글로 페이지 이동 (위의 href와 같다)
    location.assign("http://www.google.com");
	
    // 다음으로 페이지 이동 (전 단계(직전단계)의 이력 없애버림)
    // 따라서 뒤로가기하면 전전 단계로감. 덮어쓰기개념 
    location.replace("http://www.daum.net");	
    
	}
```

