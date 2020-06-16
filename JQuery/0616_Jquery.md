### JQuery

------



- [속성 ^ = 값] $ ( "[title ^ = 'Tom']")

  제목 속성 값이 "Tom"으로 시작하는 모든 요소

- [attribute ~ = value] $ ( "[title ~ = 'hello']")

  특정 단어 "hello"를 포함하는 title 속성 값을 가진 모든 요소

- [attribute * = value] $ ( "[title * = 'hello']")

  단어 "hello"를 포함하는 title 속성 값을 가진 모든 요소



title속성값 중, '02'를 포함하는 img 태그를 찾아서 적용 2초동안 slideUp

```javascript
$("[title *='02']").slideUp(2000);
```



스크립트의 위치따라 변하는 것 (window.onload) -> 화면 전부 그려진 뒤에 스크립트 동작

즉 html 전부 load한 뒤 스크립트 동작

$function 도 window.onload와 같음



- checkbox value가져와서 bold 처리 (.html)

```javascript
var doc = $("input:checkbox").val();
		

$("#a").html("<b>"+doc+"</b>");

// .text하면 html태그 동작 하지 않음
$("#a").text("<b>"+doc+"</b>");
```



-  라디오버튼이 체크되면 해당 버튼의 value를 가져옴

```javascript
var doc = $("input:radio").val();
```



- input의 타입이 text인 태그의 value를 가져오쟈

```javascript
var doc = $("input:text").val();
```



- onclick = "" 로 불러오는 function(){}	 = 	javascript 문법

- $(function(){

  ​	작성					=   jQuery 문법 (명령문 단독 사용 불가)

  })



```javascript
$(function(){
		var selElem = document.getElementsByTagName("select")[0];
		selElem.onchange=function(){
			alert(selElem.options[selElem.selectedIndex].value);
		}
	});
```

JQuery로 변경 ->

```javascript

```





- .attr("Attr Name") / .prop("Prop Name") : 엘리먼트의 속성 값

- .attr() : HTML의 속성 (attribute)를 (HTML의 속성을 건드림, HTML에 접근함)

- .prop() : Javascript의 프로퍼티(property)를 취급하는 메서드 (HTML에서는 변화가 없음)

- each : 각각 객체 하나하나에 무언가를 준다

  

------



#### 속성을 추출해서 다른 속성에 넣는법 ( for, .each() )

- 하단의 html태그에서 title 속성을 추출해 각각의 td>img태그의 src속성으로 넣어

  이미지를 순서대로 변경하고 싶었음.

  G:\git_test\Javascript\jq_selector_1.html

```javascript
function changeImg(){
            //원본의 답.
            //$("td > img").attr("src","resources/img/img02.jpg");
		
        // 각각의 value대로 img가 변경
            

            $("td>img").each(function(){
                //console.log($(this).attr("title"));
                var src = $(this).attr("title")
                $(this).attr("src","resources/img/"+src+".jpg");
            })

            // 실패.. 이럴때 .each를 쓰면 간단해짐.
            // for(var i = 0; i <= $("td").length; i++){     
                
            //     if(td.eq(i).has(">img")){
            //         ele = $(td.eq(i)).children("img").attr("title");                    
            //         $("td>img").attr("src","resources/img/"+ele+".jpg");
            //         console.log(ele);
            //     }
            // }            

//완본
// var td1 = document.getElementsByTagName("td");
// for(var i = 0; i < td1.length; i++) {
// $("img[title=img0"+i+"]").attr("src","resources/img/img0"+i+".jpg");
// }		
	    }
```

```html
<table>
	<tr>
		<td><img src="resources/img/img01.jpg" title="img01" id="selId"></td>
		<td><img src="resources/img/img01.jpg" title="img02"></td>
		<td><img src="resources/img/img01.jpg" title="img03" class="selClass"></td>
		<td><img src="resources/img/img01.jpg" title="img04" class="selClass"></td>
	</tr>
	<tr>
		<td><img src="resources/img/img01.jpg" title="img05" id="selId"></td>
		<td><span><img src="resources/img/img01.jpg" title="img06"></span></td>
		<td><span><img src="resources/img/img01.jpg" title="img07" class="selClass"></span></td>
		<td><img src="resources/img/img01.jpg" title="img08" class="selClass"></td>
	</tr>
</table>
```

