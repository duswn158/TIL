## Checked



>##### script
>
>```javascript
>function allChk(bool){
>	var chks = document.getElementsByName("chk");
>	for (var i = 0; i < chks.length; i++){
>		chks[i].checked = bool;
>	}
>}
>	
>function disallchk(){
>// name 이 chk인 태그들의 length
>//console.log($("[name=chk]").length, $("input[name=chk]:checked").length);	
>		
>// 하나라도 클릭시 전체선택 해제 모두 선택하면 자동으로 전체선택 체크박스도 선택
>	if ($("input[name=chk]").length == $("input[name=chk]:checked").length){
>		$("input:checkbox[name=all]").prop("checked", true);
>	} else {
>
>        // 아래와 같은 경우일때 위에서 넣은 checked 속성이
>        // html에 있는게 아니기 때문에 attr로 바꾸어 줄 수 없음
>        //$("input:checkbox[name=all]").attr("checked", false);
>			
>		$("input:checkbox[name=all]").prop("checked", false);
>		//console.log($("input:checkbox[name=all]"));
>	};
>		
>}
>	
>	
>$(function(){
>		
>	//alert("onload");
>	$("[name=chk]").click(function(){
>		disallchk()
>	});
>});
>```
>
>
>
>
>
>##### HTML & JSTL
>
>```jsp
><h1>글 목록</h1>
>	
>	<table border="1">
>		<col width="50">
>		<col width="50">
>		<col width="300">
>		<col width="100">
>		<col width="100">
>		
>		<tr>
>			<th><input type="checkbox" name="all" onclick="allChk(this.checked);"></th>
>			<th>번 	호</th>
>			<th>제	목</th>
>			<th>작 성 자</th>
>			<th>작 성 일</th>
>		</tr>
>		
>		<c:choose>
>			<c:when test="${empty list }">
>				<tr>
>					<td colspan="5" align="center">--------------작성된 글이 존재하지 않습니다-----------</td>
>				</tr>
>			</c:when>
>			<c:otherwise>
>				<c:forEach items = "${list }" var="dto">
>					<c:choose>
>						<c:when test="${dto.delflag eq 'Y' }">
>							<tr>
>								<td colspan="5" align="center">--------------작성된 글이 존재하지 않습니다-----------</td>
>							</tr>
>						</c:when>
>						<c:otherwise>
>							<tr>
>								<td><input type="checkbox" name="chk" value="${dto.boardno }"></td>
>								<td>${dto.boardno }</td>
>								<td>	
>									<c:forEach begin="1" end ="${dto.titletab }">
>										&nbsp;
>									</c:forEach>
>									<a href="controller.do?command=detail&boardno=${dto.boardno }">${dto.title }</a>									
>								</td>
>								<td>${dto.writer }</td>
>								<td>${dto.regdate }</td>		
>							</tr>
>						</c:otherwise>
>					</c:choose>
>				</c:forEach>
>			</c:otherwise>
>		</c:choose>
>		<tr>
>			<td colspan="5" align="right">
>				<input type="button" value="글작성" onclick="location.href='controller.do?command=insert'">
>				<input type="button" value="선택삭제" onclick="">
>			</td>
>		</tr>		
>	</table>
>```
>
>



##### 기타 참고 (선택자 등등): 

>https://m.mkexdev.net/145
>
>https://dh-dh.tistory.com/31
>
>https://araikuma.tistory.com/607