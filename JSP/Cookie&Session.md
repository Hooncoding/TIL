쿠키와 세션
==============
## introduction
클라이언트와 서버는 http 프로토콜을 통해 요청 응답을 수행한다.  
그런데, 위 행위는 서버가 응답을 전송할 시 끝나는 일회성 통신이다.  
그래서, 요청 - 응답간의 정보를 저장하고, 클라이언트 - 서버 간 연결을 지속적으로 유지해줄 장치가 필요하다.  
이러한 기능을 하는 것이 바로 쿠키와 세션이다.  

## What is Cookie?  
쿠키는 클라이언트 측에서 관리되는 임시 파일이다.  
1. 쿠키는 클라이언트의 하드디스크에 저장되며 4kb 정도의 용량을 가진다.
2. 쿠키는 클라이언트 - 서버 간 발생하는 정보들을 저장한다.
3. 쿠키는 유효 기간이 있다. (그래서 임시 파일이라는 말을 썼다.)
4. 쿠키는 name과 value로 이루어져 있으며 HashMap 형태로 저장된다.

## Why Using Cookie?  
Intro에서 짧게 언급했듯이 쿠키는 저장와 유지의 역할을 한다.  
1. 저장: 클라이언트 - 서버 간 통신에 의해 발생한 정보를 저장한다.
2. 유지: 쿠키의 name이나 value를 이용해 클라이언트 - 서버 간 연결을 유지할 수 있다.

예를 들어, 한 사이트에 로그인하여 사이트 내 컨텐츠를 이용하려는 유저가 있다고 가정한다.  
1. 유저는 로그인 창을 통해 자신의 id와 password를 입력하고 로그인 버튼을 누른다.
2. 서버는 DB 내에 해당 유저가 입력한 id / pw가 일치하는지 확인하고 일치할 경우 welcome 페이지로 이동시킨다.

그런데, 이게 끝이다. 유저는 welcome 페이지만 볼 수 있고 welcome 페이지를 벗어나는 컨텐츠를 이용할 수 없다.  
그 이유는, 2번에서 서버가 응답을(welcome 페이지로 redirect) 전송할 시 1번에서 입력한 id / pw 정보는 삭제된다.  
즉, welcome에서 다른 페이지로 이동할 경우 서버는 다시 유저에게 id / pw 정보를 요청할 것이다. 컨텐츠를 이용할 때마다 로그인을 다시 해야하는 상황인 것이다.

따라서, 유저가 사이트를 떠나기 전까지 해당 유저의 로그인 정보를 보관할 저장소가 필요하다. => 이게 바로 쿠키!

## Cookie 관련 주요 메소드  
- setMaxage(int) => 쿠키의 유효 기간을 설정한다.
- getValue() => 쿠키에 설정된 값을 가져온다.


## 예제 코드: Cookie를 통해 로그인 유지하기  
편의상 html, head, body 태그 등 기본 태그는 생략합니다.  

1. 로그인 페이지 (loginForm.jsp)

```
  <form action="loginOK.jsp" method="post"> //사실 servlet이어야 하지만 편의상 jsp 파일로 한다.
  
  아이디 :   <input type="text" name="id"> </br>
  비밀번호 : <input type="password" name="pw"> </br>
            <input type="submit" value="로그인"> </br>            
  </form>
```

2. 로그인 처리 페이지 (loginOK.jsp)
```
  String id = request.getParameter("id");
  String pw = request.getParameter("pw");
  
  if(id.equals("홍길동") && pw.equals("1234")){ //원래는 DB에 저장되어 있는 id/pw값과 비교해야 하나, 편의상 생략
    Cookie[] cookie = new Cookie("id", id); // id란 이름을 가지고, 회원의 id 정보(홍길동)를 저장한 cookie 객체 생성.
    cookie.setMaxage(60); //쿠키의 유효시간 : 60초
    response.addCookie(cookie); // cookie 객체를 response에 추가 (이게 없으면 홍길동의 로그인 정보는 삭제된다)
    response.sendRedirect("welcome.jsp"); // 로그인 성공시 유저를 welcome.jsp 페이지로 보낸다.
  }else{
    response.sendRedirect("loginForm.jsp"); // 로그인 실패시 다시 로그인하게 한다.
  }
```

3. Welcome 페이지 (welcome.jsp)
```
  Cookie[] cookies = request.getCookies();
  for(int i=0; i < cookies.length(); i++){
    String id = cookies[i].getValue();
    
    if(id.equals("홍길동")){ // Cookie가 홍길동이라는 로그인 정보를 저장하고 있어서 환영 메세지를 받을 수 있다.
    out.println(id + "님 환영합니다");
    }else{
    response.sendRedirect("loginForm.jsp");
  }
```

결론적으로, Cookie가 홍길동 user의 로그인 정보를 저장하고 있기 때문에 설정한 60초간 홍길동은 사이트에서 별도의 재로그인이 필요 없이 컨텐츠를 이용할 수 있다.

## What is Session? 
세션의 기능은 쿠키와 동일하나 서버 측에서 관리 및 저장된다. 이로 인해 쿠키와는 다른 특성을 가진다.
1. 쿠키는 크기가 4kb로 제한되나, 세션은 이론상 서버 용량과 같은 크기이다. (쿠키보다 더 많은 정보를 저장할 수 있다.)
2. 보안상 강점이 있다. (쿠키는 해커가 하드디스크를 털면 바로 나오지만, 서버 컴퓨터는 개인 컴퓨터보다 보안이 뛰어나다.)

## Session 관련 주요 메소드
- setAttribute() 세션에 데이터 저장
- getAttribute() 세션에서 데이터 추출
- inValidate() 세션 내 모든 데이터 삭제
