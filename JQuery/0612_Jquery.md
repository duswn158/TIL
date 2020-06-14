### JQUERY

------

제이쿼리 홈페이지

https://jquery.com/ 에서 설치.



[Download the compressed, production jQuery 3.5.1 slim build](https://code.jquery.com/jquery-3.5.1.slim.min.js)

크기 : 87.3

jquery-3.5.1.min.js



[Download the uncompressed, development jQuery 3.5.1 slim build](https://code.jquery.com/jquery-3.5.1.slim.js)

크기 : 280

jquery-3.5.1.js



오른쪽 클락 + 다른이름으로 링크 저장. jquery-3.5.1.min.js파일 저장됨

커스터 마이징 할수 있도록 공백포함된 파일도 제공함



jquery 기본 작성법!

```javascript
 	css selector(표현식) + javascript
 	작성 예)
 		$("selector").메서드();
 		$("p").css("color","red");
```



기능 구현 2가지 방법!!

```javascript
	//1.
 	$(function(){
 		//작성
 	});
 	
 	//2.
 	$(document).ready(function(){
 		//작성
 	});
```



이미지 만들어서 추가 (<img src = 'resources/img/img01.jpg'>)

```javascript
function addImg(){ 		
 		var addimg = "<img src = 'resources/img/img02.jpg'>";
 		$("img").last().after("<img src='resources/img/img02.jpg'>");
 	}
```

