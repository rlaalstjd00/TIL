## Front-Controller 패턴

#### Front-Controller 특징

- 서블릿 하나로 클라이언트의 요청을 받음
- 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출
- 프론트 컨트롤러 외의 나머지 컨트롤러는 서블릿을 사용하지 않아도 됨

<img src="..\99_img_src\FrontController.PNG" width="650">

#### URL 매핑

게시판에 추가 수정 삭제 조회 하는 기능을 구현 한다고 가정해보자.

각각의 url들은 모두

- ../proj/board/register
- ../proj/board/modify
- ../proj/board/remove
- ../proj/board/get

과 같이 모두 다르기 때문에 한 서블릿에 매핑할 수 없다.

따라서 url을 ../proj/board/* 와 같은 형식으로 설정해주면 ../proj/board 를 포함한 하위 모든 요청들을 찾을 수 있게 된다.



#### Front-Controller 작동방식

<img src="..\99_img_src\FrontController2.PNG" width="650">

> 위의 작동방식은 기존의 서블릿이나 JSP를 통한 MVC 패턴보다 발전된 형태이다.
>
> 그러나 Front Controller가 한 가지 타입의 컨트롤러만 호출할 수 있다는 단점이 있다. 따라서 여러 컨트롤러의 인터페이스와 호환 가능하도록 어댑터 패턴이라는 것을 도입한다.



#### 어댑터 패턴을 도입한 MVC 패턴

<img src="..\99_img_src\FrontController3.PNG" width="650">



> 어댑터 패턴을 도입하기 이전에는 Front Controller가 직접 컨트롤러를 호출했다. 그러나 어댑터 패턴을 도입한 후에는 중간에 핸들러 어댑터가 새로 들어가서 매개변수로 넘어온 핸들러가 지원 가능한 핸들러인지 확인한 후, 실제 핸들러(컨트롤러)를 호출하고 결과로 ModelView를 반환하게 된다.
