JSTL(JSP Standard Tag Library)
=============================

What is JSTL
-------------
JSTL은 라이브러리다. 라이브러리란 이미 만들어진 부품이다.
라이브러리는 보통 유용한 기능이 있다.
JSTL은 표현식 없이도 JSP 내 자바코드를 사용할 수 있는 기능을 한다.
JSTL 태그를 이용하려면 JSTL 라이브러리를 임포트 해야한다.

JSTL vs 표현식
-------------
아래 두 코드는 JSP 내에서 같은 결과를 도출한다.

**변수 값 선언(표현식 사용)**
```
<% String name = "dylan" %>
```

**변수 값 선언(JSTL 사용)**
```
<c:set var="name" value="dylan"/>
```

**변수 값 출력(표현식 사용)**
```
<%out.println(name) %>
```

**변수 값 출력(JSTL 사용)**
```
<c:out value="$(name)"/>
```

이외에도 조건문, 반복문 등 다양한 tag를 사용할 수 있다.
