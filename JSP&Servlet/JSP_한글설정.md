### JSP 파일 한글설정

> 1. jsp파일 생성시 next버튼 누르고 JSP Templates 링트를 누르고 -> JSP Files에서 UTF-8로 변경가능
>
> 2. 동일한 경로에서 Templates -> New JSP File(html 5) 클릭 -> 오른쪽에 Edit.. 버튼 ->     
>    <% request.setCharacterEncoding("${encoding}") %>
>    <% response.setContentType("text/html; charset=${encoding}"); %> 
>
>    두가지 입력 



servlet 한글 깨지는 에러 대비 :

```jsp
<!-- 요청하는 객체의 문자열을 UT_8로 바꾸자 -->
<% request.setCharacterEncoding("UTF-8"); %>
<!-- 응답해줄때 text지만 html이고, 문자열을 UTF-8이다  -->
<% response.setContentType("text/html; charset=UTF-8"); %>
```


