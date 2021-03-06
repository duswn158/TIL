# JSTL



#### JSTL 이란?

JSTL은 JSP 표준라이브러리(JSP Standard Tag Library)의 약어이다. 자주 사용될 수 있는 커스텀 태그들을 모아서 표준으로 모아놓은 태그 라이브러리다.



#### JSTL 의 종류

| 라이브러리명 | 접두어 | 주요 기능                           | URI                                   |
| ------------ | ------ | ----------------------------------- | ------------------------------------- |
| 코어         | c      | 변수 지원, 제어문, 페이지 관련 처리 | http://java.sun.com/jsp/jstl/core     |
| 함수         | fn     | collection 처리, String 처리        | http://java.sun.com/jsp/jstl/fuctions |
| 포매팅       | fmt    | 포맷 처리, 국제화 지원              | http://java.sun.com/jsp/jstl/fmt      |
| 데이터베이스 | sql    | DB관련 CRUD 처리                    | http://java.sun.com/jsp/jstl/sql      |
| XML          | x      | XML관련 처리                        | http://java.sun.com/jsp/jstl/xml      |

### 사용법

위의 표에서 참고하여 JSP 상단에 `<%@ taglib prefix="접두어" uri="URI 경로" %>` 를 적어주면 된다. 접두어야 마음대로 쓸 수 있는 모양이지만 기왕이면 표준을 지키는게 좋다..



## 2. core 의 주요 기능

- `<c:set>` : 변수 선언, 할당

  - scope 속성 : 범위 4가지(page, request, session, application), default 는 page
  - ex. int count = 10; = `<c:set var="count" value="10">`

- `<c:out>` : 출력

  - ex. System.out.println("hello");을 간단하게 `<c:out value="hello">`

- `<c:remove>` : 변수값 remove

  - scope 속성

- `<c:if>` : if문, else문 없음

  - var 속성 : 조건식의 값을 저장할 변수
  - scope 속성 : boolean 변수가 사용될 범위를 뜻함
  - ex. `<c:if test="조건식"> 참일때 실행할 문장 </c:if>`

- `<c:choose>, <c:when>, <c:otherwise>` : if-else 문 처럼 사용 가능

  - when 이 true 이면 해당 블럭 실행

  - 모든 when 이 false 이면 otherwise 블럭 실행

    ```
      <c:choose>
          <c:when test="${empty boardList}">
              등록된 글이 없습니다.
          </c:when>
          <c:when test="조건식">
              ...
          </c:when>
          <c:otherwise>
              ...
          </c:otherwise>
      </c:choose>
    ```

- `<c:forEach>` : for문이다

  | 속성      | 설명                              | 비고     |
  | --------- | --------------------------------- | -------- |
  | var       | 사용할 변수명                     | Required |
  | items     | Collection 객체(List, ArrayList)  | Required |
  | begin     | 시작 index(default = 0)           |          |
  | end       | 종료 index(default = items크기-1) |          |
  | step      | 증감 수                           |          |
  | varStatus | 반복상태를 알 수 있는 변수        |          |

  ```
    <c:forEach var="item" items="${list}" begin=0 end=5 step=1 varStatus="status">
        번호 : ${status.count}
        이름 : ${item.name}
        나이 : ${item.age}
        주소 : ${item.addr}
    </c:forEach>
  ```

## 3. fuctions 의 주요 기능

- boolean startsWith(java.lang.String, java.lang.String) : 문자열A가 문자열B로 시작하는 경우, true 반환
  - ex. `<a class="<c:if test="${fn:startsWith(servletPath, '/board')}">active</c:if>" href="/board">`



출처: https://sjh836.tistory.com/136 [빨간색코딩]







### \<c:out> 태그

**문법**

```jsp
<c:out value="출력할 값" default="기본값/>
또는
<c:out value="출력할 값">기본값\</c:out>
```



### \<c:set> 태그

**문법**

```jsp
value 속성을 사용하여 값 설정
<c:set var="변수명" value="값" scope="page|request|session|application"/>
태그 콘텐츠를 사용하여 값 설정
<c:set var="변수명" scope="page|request|session|application"/>값\</c:set>
```



### \<c:remove> 태그

**문법**

```jsp
value 속성을 사용하여 값 설정
<c:remove var="변수명" scope="page|request|session|application"/>
```



### \<c:if> 태그

**문법**

```jsp
<c:if teset="조건" var="변수명" scope="page|request|session|application">
콘텐츠
</c:if>

<c:if test="${10 > 20}" var="result1">
10은 20보다 크다.
</c:if>
${result1}

//결과
//false
```



### \<c:choose> 태그

**문법**

```jsp
<c:choos>
	<c:when test="참거짓 값"></c:when>
	<c:when test="참거짓 값"></c:when>
	....
	<c:otherwise></otherwise>
</c:choose>

<c:set var="userid" value="hong"/>
<c:choose>
  <c:when test="${userid == 'hong'}">
    홍길동님 반갑습니다.
  </c:when>
  <c:when test="${userid == 'leem'}">
    임꺽정님 반갑습니다.
  </c:when>
  <c:when test="${userid == 'admin'}">
    관리자 전용 페이지입니다.
  </c:when>
  <c:otherwise>
    등록되지 않은 사용자입니다.
  </c:otherwise>
</c:choose>

//결과
//홍길동님 반갑습니다.
```



### \<c:forEach> 태그

**문법**

```jsp
<c:forEach var="변수명" item="목록데이터" begin="시작인덱스" end="종료인덱스">
	콘텐츠
</c:forEach>

<h3>반복문 - 배열</h3>
<% pageContext.setAttribute("nameList", 
  new String[]{"홍길동", "임꺽정", "일지매"}); %>
<ul>
<c:forEach var="name" items="${nameList}">
	<li>${name}</li>	
</c:forEach>
</ul>

<h3>반복문 - 배열의 시작 인덱스와 종료 인덱스 지정</h3>
<% pageContext.setAttribute("nameList2", 
  new String[]{"홍길동", "임꺽정", "일지매", "주먹대장", "똘이장군"}); %>
<ul>
<c:forEach var="name" items="${nameList2}" begin="2" end="3">
	<li>${name}</li>	
</c:forEach>
</ul>

<h3>반복문 - ArrayList 객체</h3>
<% 
ArrayList<String> nameList3 = new ArrayList<String>();
nameList3.add("홍길동");
nameList3.add("임꺽정");
nameList3.add("일지매");
nameList3.add("주먹대장");
nameList3.add("똘이장군");
pageContext.setAttribute("nameList3", nameList3); 
%>
<ul>
<c:forEach var="name" items="${nameList3}">
	<li>${name}</li>	
</c:forEach>
</ul>

<h3>반복문 - 콤마로 구분된 문자열</h3>
<% pageContext.setAttribute("nameList4", "홍길동,임꺽정,일지매,주먹대장,똘이장군"); %>
<ul>
<c:forEach var="name" items="${nameList4}">
	<li>${name}</li>	
</c:forEach>
</ul>

<h3>반복문 - 특정 횟수 만큼 반복</h3>
<ul>
<c:forEach var="no" begin="1" end="6">
	<li><a href="jstl0${no}.jsp">JSTL 예제 ${no}</a></li>	
</c:forEach>
</ul>
```



### \<c:forTokens> 태그

문자열을 특정 구분자(delimiter)로 분리하여 반복문을 돌릴 수 있다.

```jsp
<% pageContext.setAttribute("tokens","v1=20&v2=30&op=+"); %>
<ul>
<c:forTokens var="item" items="${tokens}" delims="&">
	<li>${item}</li>	
</c:forTokens>
</ul>

/*
결과
v1=20
v2=30
op=+
*/
```

이밖에도 <c:url>, <c:import>, <c:redirection>, <fmt:parseData> 등 많은 태그들이 있다.





출처 : https://joswlv.github.io/2016/09/13/jsp_tag/



## **fmt태그의 종류**



| **기능**           | **태그**                                                    | **설명**                                     |
| ------------------ | ----------------------------------------------------------- | -------------------------------------------- |
| **숫자 날짜 형식** | formatnumber                                                | 숫자를 양식에 맞춰서 출력한다.               |
| formatDate         | 날짜 정보를 담고 있는 객체를 포맷팅하여 출력할 때 사용한다. |                                              |
| parseDate          | 문자열을 날짜로 파싱한다.                                   |                                              |
| parseNumber        | 문자열을 수치로 파싱한다.                                   |                                              |
| setTimeZone        | 시간대별로 시간을 처리할 수 있는 기능을 제공한다.           |                                              |
| timeZone           | 시간대별로 시간을 처리할 수 있는 기능을 제공한다.           |                                              |
| **로케일 지정**    | setLocale                                                   | 국제화 태그들이 사용할 로케일을 지정한다.    |
| requestEncoding    | 요청 파라미터의 인코딩을 지정한다.                          |                                              |
| **메시지 처리**    | bundle                                                      | 태그 몸체에서 사용할 리소스 번들을 지정한다. |
| message(param)     | 메시지를 출력한다.                                          |                                              |
| setBundle          | 특정 리소스 번들을 사용할 수 있도록 로딩한다.               |                                              |



#### ▶ \<fmt:formatDate>

> 날짜를 2013.08.22와 같은 형태로 출력하고자 할 경우 사용됨.
>
> value속성에 date를 넣어서 처리하기 위해서는 java.util.Date 클래스로 객체를 생성하는 것이 필수적이다.
>
> **- 선행조건**
>
> : <c:set var="now" value="<%=new java.util.Date()%>"/>
>
> ##### \<fmt:formatDate value="date"
>
> [**type** = "{time| date| both}"]
>
> [**dateStyle**="{default | short | medium | long | full}"]
>
> [**timeStyle**="{default | short | medium | long | full}"]
>
> [**pattern**="customPattern"]
>
> [**timeZone**="timeZone"]
>
> [**var**="변수 이름"]
>
> [**scope**="{page | request | session | application}"] **>**
>
> | **속성**      | **표현식** | **타입**                   | **설명**                                                     |
> | ------------- | ---------- | -------------------------- | ------------------------------------------------------------ |
> | **value**     | true       | java.util.Date             | 형식화될 Date와 time                                         |
> | **type**      | true       | String                     | 형식화할 데이터 타입 셋 중 하나를 지정1. 시간(time) 2. 날짜(date) 3. 모두(both) |
> | **dateStyle** | true       | String                     | 미리 정의된 날짜 형식으로 default \| short \| medium \| long \| full 중 하나 지정. |
> | **timeStyle** | true       | String                     | 미리 정의된 날짜 형식으로 default \| short \| medium \| long \| full 중 하나 지정. |
> | **pattern**   | true       | String                     | 사용자 지정 형식 스타일                                      |
> | **timeZone**  | true       | String 또는 java.util.Date | 형식화 시간에 나타날 타임존                                  |
> | **var**       | false      | String                     | 형식 출력 결과 문자열을 담는 scope에 해당하는 변수 이름      |
> | **scope**     | false      | String                     | var 속성에 지정한 변수가 효력을 발휘할 수 있는 영역 지정     |
>
> 
>
> 참조 : https://m.blog.naver.com/PostView.nhn?blogId=imf4&logNo=220654812087&proxyReferer=https:%2F%2Fwww.google.com%2F

