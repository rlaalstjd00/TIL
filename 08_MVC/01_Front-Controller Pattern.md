## Front-Controller 패턴

#### Front-Controller 특징

- 서블릿 하나로 클라이언트의 요청을 받음
- 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출
- 프론트 컨트롤러 외의 나머지 컨트롤러는 서블릿을 사용하지 않아도 됨

> a.jsp --> web.xml --> Servlet (FrontController.java)
>
> 　　　　　　　　　　　　　　　↓
>
> 　　　　　　　　　　　if, switch문으로 분기
>
> 　　　　　　　　　　　　　　　↓
>
> 　　　　　　　　　　　Controller (~~Action)

#### web.xml 매핑

게시판에 추가 수정 삭제 조회 하는 기능을 구현 한다고 가정해보자.

각각의 url들은 모두

- ../board_proj/register
- ../board_proj/modify
- ../board_proj/remove
- ../board_proj/get

과 같이 모두 다르기 때문에 한 서블릿에 매핑할 수 없다.

따라서 url을 ../board_proj/register.bo 와 같은 형식으로 설정해주면 서블릿에 *.bo 로 매핑해 모두 찾을 수 있다. 그리고 '.' 을 기준으로 앞에 무엇이 있냐에 따라 `if`나 `switch` 문을 이용해 추가 수정 조삭제 조회를 나눠서 기능구현할 수 있다.

#### Front-Controller 작동방식

1. 개발자가 정의한 확장자를 페이지 이동 주소에 작성하게 되면 파일이 아니므로 web.xml에 가서 매핑되어 있는 서블릿으로 찾는다.

   (앞서 예시와 같이 *.bo로 서블릿에 매핑해놓았다고 가정하자.)

2. 어떤 것이든 .bo가 붙은 요청은 BoardFrontController로 이동하게 매핑 해놓게 되면 이 프론트 컨트롤러는 .bo 앞에 있는 요청명으로 어떤 로직을 수행할지 분기처리 한다. (`if`나 `switch`문)

3. 각각에 요청별로 따로 컨트롤러를 만들어 놓고 그 안에 `execute()` 메서드를 만들어 그 내부에 비즈니스 로직을 구현한다. 그러면 프론트 컨트롤러에서는 분기에 맞는 컨트롤러의 `execute()` 메서드를 호출만 하면 되는 것이다.

   (보통 컨트롤러를 만들 때, BoardRemoveAction 과 같이 ~Action 으로 이름을 정하게 된다. 그리고 Action 이라는 인터페이스에 `execute()` 추상메서드를 선언해 놓고 각 ~Action 컨트롤러 마다 재정의 해서 사용하면 편하다.)

#### Model 2 에서의 페이지 이동방식

JSP와 서블릿에서 페이지 이동을 처리할 때 두가지 방식중 하나를 사용한다.

a.jsp 에서 b.jsp로 이동한다고 가정할 때,

- **Redirect**

  - 서버에게 요청 -> 서버는 "b.jsp로 갈 수 있는 요청" 을 응답 -> 받은걸 이용해서 b.jsp 요청 -> b.jsp 응답 

    (요청과 응답이 두번씩 발생한다.)

  - 클라이언트가 요청했을 때 이전의 req, resp 객체는 초기화된다.

  - Insert, Update, Delete 같이 시스템에 변화가 생기는 요청은 redirect를 이용한다.

  

- **Forward**

  - 서버에게 요청 -> 서버는 처리 결과를 가지고 b.jsp 전송 -> 전송받은 곳에서 클라이언트에게 응답.

    (요청과 응답이 한번씩만 발생한다.)

  - 클라이언트에게 request 객체를 통해 값을 넘겨주어야 할 때 혹은 Select 같이 단순 조회를 할 때 사용한다.

  - Redirect보다 성능이 좋다.

#### Front-Controller 예제

[Front-Controller 구조를 이용해 회원가입 구현](https://github.com/rlaalstjd00/Web_practice/tree/master/02_frontController_prac)

