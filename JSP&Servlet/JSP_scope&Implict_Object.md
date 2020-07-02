### JSP 페이지의 내장 객체(Implict Object)

------



\- 내장 객체는 JSP 페이지 내에서 제공하는 특수한 레퍼런스 타입의 변수이다.

\- JSP 페이지에서 사용하게 되는 특수한 레퍼런스 타입의 변수가 아무런 선언과 객체 생성 없이 사용할 수 있는 이유는 JSP 페이지가 서블릿으로 변환될 때 JSP 컨테이너가 자동적으로 제공을 하기 때문이다.





JSP 페이지의 내장 객체

| 내장 객체   | 리턴 타입(Return Type)                 | 설명                                                         |
| ----------- | -------------------------------------- | ------------------------------------------------------------ |
| request     | javax.servlet.http.HttpServletRequest  | 웹 브라우저의 요청 정보를 저장하고 있는 객체                 |
| response    | javax.servlet.http.HttpServletResponse | 웹 브라우저의 요청에 대한 응답 정보를 저장하고 있는 객체     |
| out         | javax.servlet.jsp.jsp.jspWriter        | JSP 페이지에 출력할 내용을 가지고 있는 출력 스트림 객체이다. |
| session     | javax.servlet.http.HttpSession         | 하나의 웹 브라우저의 정보를 유지하기 위한 세션 정보를 저장하고 있는 객체 |
| application | javax.servlet.ServletContext           | 웹 어플리케이션 Context의 정보를 저장하고 있는 객체          |
| pageContext | javax.servlet.jsp.PageContext          | JSP 페이지에 대한 정보를 저장하고 있는 객체                  |
| page        | java.lang.Object                       | JSP 페이지를 구현한  자바 클래스 객체                        |
| config      | javax.servlet.ServletConfig            | JSP 페이지에 대한 설정 정보를 저장하고 있는 객체             |
| exception   | java.lang.Throwable                    | JSP 페이지서 예외가 발생한 경우에 사용되는 객체              |



\- 내장 객체의 속성(attribute)과 관련된 메소드

| 메소드                                 | 리턴 타입             | 설명                                                         |
| -------------------------------------- | --------------------- | ------------------------------------------------------------ |
| setAttribute(String key, Object value) | void                  | 해당 내장 객체의 속성(attribute)값을 설정하는 메소드로, 속성명에 해당하는 key 매개 변수에, 속성값에 해당하는 value 매개 변수의 값을 지정한다. |
| getAttributeNames()                    | java.util.Enumeration | 해당 내장 객체의 속성(attribute)명을 읽어오는 메소드로, 모든 속성의 이름을 얻어낸다. |
| getAttribute(String key)               | Object                | 해당 내장 객체의 속성(attribute)명을 읽어오는 메소드로, 주어진 key 매개 변수에 해당하는 속성명의 값을 얻어낸다. |
| removeAttribute(String key)            | void                  | 해당 내장 객체의 속성(attribute)을 제거하는 메소드로, 주어진 key 매개 변수에 해당하는 속성명을 제거한다. |



출처: https://hyeonstorage.tistory.com/78 





### **JSP 내장 기본 객체의 영역(scope)**

------

\- 웹 어플리케이션은 page, request, session, applicaition 이라는 4개의 영역을 가지고 있다.

\- 기본 객체의 영역은 객체의 유효기간이라고도 불리며, 객체를 누구와 공유할 것인가를 나타낸다.



**(1) page 영역**

\- page 영역은 한 번의 웹 브라우저(클라이언트)의 요청에 대해 하나의 JSP 페이지가 호출된다.

\- 웹 브라우저의 요청이 들어오면 이때 단 한 개의 페이지만 대응이 된다.

\- 따라서 page 영역은 객체를 하나의 페이지 내에서만 공유한다.

\- page 영역은 pageContext 기본 객체를 사용한다.





**(2) request 영역**

\- **요청한 영역까지만 살아있다. (a.jsp에서 b.jsp로 요청하여도 실제 요청을 하는곳은 서버이기 때문에 서버까지만 살아있음)**

\- request 영역은 한 번의 웹 브라우저(클라이언트)의 요청에 대해 같은 요청을 공유하는 페이지가 대응된다. 

\- 이것은 웹 브라우저의 한 번의 요청에 단지 한 개의 페이지만 요청될 수 있고, 때에 따라 같은 request 영역이면 두 개의 페이지가 같은 요청을 공유할 수 있다.

\- 따라서 request 영역은 객체를 하나 또는 두 개의 페이지 내에서 공유할 수 있다.

\- include 액션 태그, forward 액션 태그를 사용하면 request 기본 객체를 공유하게 되어서 **같은 reqeust 영역이 된다.**

\- 주로 페이지 모듈화에 사용된다.



**(3) session 영역**

\- session 영역은 하나의 웹 브라우저 당 1개의 session 객체가 생성된다.

\- 즉, 같은 웹 브라우저 내에서는 요청되는 페이지들은 같은 객체를 공유학 ㅔ된다.



**(4) application 영역**

\- application 영역은 하나의 웹 어플리케이션 당 1개의 applicaition 객체가 생성된다.

\- 즉, 같은 웹 어플리케이션에 요청되는 페이지들은 같은 객체를 공유한다.



출처: https://hyeonstorage.tistory.com/88 





### scope 설명2

------



###### ![](\Scope2.png)

위의 그림처럼, Servlet과 JSP에서는 **Page, Request, Session, Application**의 4가지 Scope이 있다.



**1) (JSP) Page scope**

실제 선언된 JSP 페이지 내에서만 사용할 수 있는 것. 페이지 내에서 지역변수처럼 사용.



- **PageContext** 추상 클래스를 사용한다.

- JSP 페이지에서 pageContext라는 **내장 객체(Implicit Object)**로 사용 가능하다.
  다른 것 필요 없이, pageContext이름.setAttribute(), pageContext이름.getAttribute() 등의 방법으로 바로 사용하면 된다.

- **forward**가 될 경우 해당 Page scope에 지정된 변수는 **사용할 수 없다**.
  어떤 페이지로 요청이 들어온 뒤, 다른 페이지로 forward 될 경우 이전 page scope내에 있던 변수는 forward 된 page scope 내에서는 사용할 수 없다.
  cf) Request는 forward와 상관 없이, 한번 요청 후 응답할 때까지 계속 유지된다.

- 사용방법은 Application scope나 Session scope, request scope와 같다.

- 마치 **지역변수**처럼 사용된다는 것이 다른 Scope들과 다른 점이다.

- pageScope은 지역변수와 별 차이가 없기 때문에 많이 쓰이지 않지만, 종종 필요한 경우가 있다.
  JSP에서 pageScope에 값을 저장한 후 해당 값을 EL 표기법 등에서 사용할 때, 지역 변수처럼 해당 JSP나 Servlet이 실행되는 동안에만 정보를 유지하고자 할 때 사용된다.





**2) Request scope**

클라이언트로부터 하나의 요청이 들어와서 서버가 일을 수행한 후 응답을 보낼 때까지, 계속 사용할 수 있는 scope. 



- Web container 안에 있는 Servlet에 대한 http 요청을, WAS가 받아서 **웹 브라우저에게 응답할 때까지** 변수값을 유지하고자 할 경우 사용한다.
- 모든 요청이 들어올 때마다, WAS는 request 객체와 response 객체를 만든다. forward 여부 등과 상관없이, <u>하나의 요청이 들어와서 응답이 나갈 때까지 계속 유지된다.</u>
- **요청한 영역까지만 살아있다. (a.jsp에서 b.jsp로 요청하여도 실제 요청을 하는곳은 서버이기 때문에 서버까지만 살아있다)**



- Servlet의 [service() 메소드가 끝날 때](Servlet_Life Cycle.md) Request Scope가 끝난다(request 객체가 없어진다).
- http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우 사용한다.
- JSP에서는 **request** 내장 변수를 사용한다.
- Servlet에서는 **HttpServletRequest** 객체를 사용한다.
- 값을 저장할 때는 request 객체의 setAttribute() 메소드를 사용한다.
  값을 읽어 들일 때는 request 객체의 getAttribute() 메소드를 사용한다.
- **사용목적**: forward 시 값을 유지하고자 사용한다.
- 앞선 forward에 대한 포스트에서, forward 하기 전에 request 객체의 setAttribute() 메소드로 값을 설정한 후, Servlet이나 JSP에게 결과를 전달하여 값을 출력하도록 하였는데, 이렇게 forward 되는 동안 값이 유지되는 것이 Request scope를 이용한 것이다.







**3) Session scope**

session 객체가 생성되고 소멸될 때까지

request는 하나의 요청과 응답이 나갈 때까지이지만, Session scope은 session 객체가 만들어져서 소멸될 때까지이므로, 하나가 아닌 여러 개의 요청이 들어와도 계속 남아있다.



- 웹 브라우저 별로 변수를 관리하고자 할 경우 사용한다. 보통 웹 브라우저를 클라이언트라고 지칭하는데, 이는 여러 개가 있을 수 있다. Session scope은 하나의 클라이언트마다 객체를 만들어서 관리하는 것이다. 따라서 session scope은 한 클라이언트 내의 여러 개의 request들을 다 cover한다.

- 웹 브라우저간의 탭 간에는 세션정보(상태정보)가 공유되기 때문에, 각각의 탭에서는 같은 session 정보를 사용할 수 있다.

- Request scope과 달리, 하나의 session scope 내에서는 하나의 request가 끝나도 해당 session 객체는 계속 유지될 것이다. 미리 지정해 놓은 시간이 초과되거나, 탭이 닫히는 경우에 session이 종료된다. 즉 request보다는 정보를 오래 유지하게 되는 것이다(☞ 상태정보 유지).

- HttpSession 인터페이스를 구현한 객체를 사용한다.

- JSP에서는 **session** 내장 변수를 사용한다.

- Servlet에서는 **HttpServletRequest**의 **getSession()** 메소드를 이용하여 session 객체를 얻는다. (여기서 Request의 메소드를 사용하는 이유는, session 객체가 어떤 클라이언트의 요청인지 알아야 하기 때문)

- 값을 저장할 때는 session 객체의 setAttribute() 메소드를 사용한다.
  값을 읽어 들일 때는 session 객체의 getAttribute() 메소드를 사용한다.

- 쇼핑몰의 장바구니처럼 사용자 별로 유지되어야 할 정보가 있을 때 사용한다.







**4) Application scope**

하나의 application이 생성되고 소멸될 때까지 계속 유지. 

Eclipse에서 하나의 Project가 하나의 Application이라고 생각하면 되고, 하나의 Server에는 여러 개의 Web application이 존재할 수 있다.



- 웹 어플리케이션이 시작되고 종료(혹은 다시 시작)될 때까지 변수를 사용할 수 있다.

- **ServletContext** 인터페이스를 구현한 객체를 사용한다.

- JSP에서는 **application** 내장 객체를 이용한다.

- Servlet의 경우는 **getServletContext()** 메소드를 이용하여 application 객체를 이용한다.

- 웹 어플리케이션 하나당 하나의 application 객체가 사용된다.

- 값을 저장할 때는 application객체의 setAttribute() 메소드를 사용한다.
  값을 읽어 들일 때는 application객체의 getAttribute() 메소드를 사용한다.

- **모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용한다.**
  하나의 application scope는 여러 클라이언트들이 사용할 수 있기 때문이다.



| **Name**    | **Accessibility**                                         | **Lifetime**                                                 |
| ----------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| Request     | Current, included, or forwarded pages                     | Until the response is returned to the user.                  |
| Session     | All requests from the same browser within session timeout | Until session timeout or session ID invalidated  (such as user quits browser). |
| Application | All request to same Web application                       | Life of container or explicitly killed  (such as container administration action). |





출처: https://starkying.tistory.com/entry/Servlet-JSP