## 달력

 \r\n : 윈도우에서 한꺼번에 엔터역할을 함

http://json-lib.sourceforge.net/ : 신뢰할만한 라이브러리 다운로드 사이트



##### json-lib 자르파일 사용시

>##### 사용하고 있는 자바버젼과 호환되는 버전이 따로있으니 잘 찾아서 넣어야함 (다 다름)
>
>제일 최신버전부터 하나하나 해보며 직접 확인해야함 (시간없을땐 구글링)
>
>json-lib : http://json-lib.sourceforge.net/
>
>
>
>Json-lib requires (at least) the following dependencies in your classpath:
>
>- jakarta commons-lang 2.5	(2.6 버전)
>
>- jakarta commons-beanutils 1.8.0 (1.9.4버전)
>
>- jakarta commons-collections 3.2.1 (3.2.2버전)
>
>- jakarta commons-logging 1.1.1 (1.2버전 최신버전.)
>
>  http://commons.apache.org/ ( Binaries 다운 tar.gz = 리눅스 압축파일임 )
>
>- ezmorph 1.0.6
>
>  http://ezmorph.sourceforge.net/



##### 해당일에 맞는 일정들만 그루핑 하는 쿼리문 (Jsp13_CalBoard)

>
>
>##### SQL
>
>```SQL
>-- MDATE 년,월,일 순으로 오름차순 해준뒤
>-- 각 일정 날짜에 맞는 글 하나씩 group by 시키고 rownum 시킴
>
>-- ROW_NUMBER() OVER( PARTITION BY @ ODER BY )
>-- @로 GROUP BY 해서, 그룹별 ROWNUM을 생성해줌
>SELECT *
>FROM
>	(SELECT 
>	(ROW_NUMBER() OVER (PARTITION BY SUBSTR(MDATE, 1, 8) ORDER BY MDATE))
>	RN, SEQ, ID, TITLE, CONTENT, MDATE, REGDATE
>	FROM CALBOARD
>	WHERE ID = 'kh'
>    -- 7월것만 보기 위함 즉 해당년도 해당 월 것만 보기 위함
>	AND SUBSTR(MDATE, 1, 6) = '202007')
>-- 제일 위에서부터 3개만 달력에 표기하기위한 WHERE문
>WHERE RN BETWEEN 1 AND 3;
>```
>
>



프로젝트 카피시 : 우클릭 + 프로퍼티스 + Web Project Setting에 보면 Context root가 원본 루트 그대로임 변경해주어야함

#####  프레임 워크 : 

> 반쯤 만들어진 프로그램 (공통부분이 완성되어있고 개발자가 특정부분을 채워넣으면 완성되는 미완성 프로그램 혹은 프로그램 틀)



## MYbatis

: 퍼시스턴스 "프레임워크"

-> JDBCTemplate (공통된 코드들을 '보일러 플레이트 코드' 라고함)

-> 마이바티스가 다른 부분들은 처리할태니 사용자(개발자)는 sql에 집중하도록 하자



https://mybatis.org/mybatis-3/ko/getting-started.html -> 읽어보기

https://mybatis.org/mybatis-3/ko/apidocs/index.html -> API



##### 마이바티스는 무엇인가?

> 마이바티스는 개발자가 지정한 SQL, 저장프로시저 그리고 몇가지 고급 매핑을 지원하는 퍼시스턴스 프레임워크이다. 마이바티스는 JDBC로 처리하는 상당부분의 코드와 파라미터 설정및 결과 매핑을 대신해준다. 마이바티스는 데이터베이스 레코드에 원시타입과 Map 인터페이스 그리고 자바 POJO 를 설정해서 매핑하기 위해 XML과 애노테이션을 사용할 수 있다.



##### 쉬운사용

>- 두가지 "" 빼고 넣고 apply
>
>
>
>이클립스에서 window - preferences - XML - XML Catalog에 가서
>
>add Location에 http://mybatis.org/dtd/mybatis-3-config.dtd 를,
>
>key에 -//mybatis.org//DTD Config 3.0//EN 를 넣어준다.
>
>
>
>config.xml과 mapper.xml의 dtd가 다르다. mapper.xml은 2번을 이걸로.
>
>key : -//mybatis.org//DTD Mapper 3.0//EN
>
>Location : http://mybatis.org/dtd/mybatis-3-mapper.dtd
>
>
>
>.<img src="mybatise_settion.png" style="zoom:50%;" />
>
>
>
>- 다 되었으면, xml 파일을 새로 생성할 때 'next' 눌러서 from a DTD file -> next -> - select a catalog entry 선택후 config, mapper 찾아서 생성
>
>  



Config file은 하나, Mapper파일은 여러개 보통 테이블 하나당 Mapper.xml 하나

**DataSource** (중요) : Connection객체를 연결해줌



### 동적 SQL

> https://mybatis.org/mybatis-3/ko/dynamic-sql.html
>
> 마이바티스의 가장 강력한 기능 중 하나는 동적 SQL을 처리하는 방법이다.** JDBC나 다른 유사한 프레임워크를 사용해본 경험이 있다면 동적으로 SQL 을 구성하는 것이 얼마나 힘든 작업인지 이해할 것이다. 간혹 공백이나 콤마를 붙이는 것을 잊어본 적도 있을 것이다. 동적 SQL 은 그만큼 어려운 것이다.
>
> 동적 SQL 을 사용하는 것은 결코 **파티가 될 수 없을 것이다**. 마이바티스는 강력한 동적 SQL 언어로 이 상황은 개선한다.



### Result Maps

> resultMap엘리먼트는 **<u>마이바티스에서 가장 중요하고 강력한 엘리먼트</u>**이다. ResultSet에서 데이터를 가져올때 작성되는 JDBC코드를 대부분 줄여주는 역할을 담당한다. 사실 join매핑과 같은 복잡한 코드는 굉장히 많은 코드가 필요하다. ResultMap은 간단한 구문에서는 매핑이 필요하지 않고 복잡한 구문에서 관계를 서술하기 위해 필요하다.
>
> 
>
> ```java
> dto에 getter 이름과 아래 구문의 이름이 같아야 하는데 만약 그러지 못할경우
>  ** Result Maps 을 만든다 (연결, 맵핑) **
>    
>    <!-- id : resultMap의 id, type : 사용할 객체 -->
>    <!-- 대소문자 구분 X -->
>    <resultMap type="myDto" id="myDtoResultMap">
> 	   	<result property="myno" column="MYNO"/>
> 	   	<result property="myname" column="MYNAME"/>
> 	   	<result property="mytitle" column="MYTITLE"/>
> 	   	<result property="mycontent" column="MYCONTENT"/>
> 	   	<result property="mydate" column="MYDATE"/>
>    </resultMap>
>    
>    <select id="selectList" resultMap="myDtoResultMap">
>   	SELECT MYNO, MYNAME, MYTITLE, MYCONTENT, MYDATE
>   	FROM MYBOARD
>   </select>
> ```
>
> 
>
> cash 말고 mapper 속성에 namespace를 잡아주어야함
>
> ```java
> <mapper namespace="com.muldel.mapper">
>   
> </mapper>
> ```
>
> 



##### typeAliases

> 타입 별칭은 자바 타입에 대한 짧은 이름이다. 오직 XML 설정에서만 사용되며, 타이핑을 줄이기 위해 존재한다.



초기설정

```java
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```



#### 순서 : 

> 
>
> 1. SqlMapConfig
>    - sqlSessionFactory를 리턴
>    - sqlSessionFactory 를 빌드하기 위함 (객체를 만듬)
> 2. Config.xml
>    - 설정들이 들어감 (전반적인 설정을 잡아줌)
>    - **DataSource**
>    - DB랑 연결
>    - Type Aliase (별칭주는 애 Type에 별칭을 줄것)
>    - Mapper
> 3. Mapper.xml
>    - SQL 쿼리문 전달해주는것 작성
>
> 
>
> ##### MVC패턴처럼 각자 하는일이 나누어져 있다.
>
> 



##### db.properties

> - 일반 파일로 만들수 있고,
> - k : v 의 형태를 취한다.
> - 주석 사용 불가
> - **" " 절대 사용불가**



##### \<configuration>

>Content Model 순서대로 미작성시 에러남
>
>Content Model : (**properties**?, settings?, **typeAliases**?, typeHandlers?, objectFactory?, 
> objectWrapperFactory?, reflectorFactory?, plugins?, **environments**?, databaseIdProvider?, 
> mappers?)



스프링부트때 쓰면 편함

>
>
>BlogMapper와 같은 Mapper클래스에는 몇가지 트릭이 있다. 매핑된 구문은 XML 에 전혀 매핑될 필요가 없다. 대신 자바 애노테이션을 사용할 수 있다. 예를들어 위 XML 예제는 다음과 같은 형태로 대체될 수 있다.
>
>```java
>package org.mybatis.example;
>public interface BlogMapper {
>  @Select("SELECT * FROM blog WHERE id = #{id}")
>  Blog selectBlog(int id);
>}
>```

