## 스프링 빈 (Spring Bean)

'빈(Bean)' 이란, 스프링 컨테이너가 관리하는 자바 객체이다.

#### 스프링 컨테이너에 빈 등록

스프링이 스프링 컨테이너에 스프링 빈을 등록할 때, 기본적으로 하나의 객체만을 등록하는 싱글톤 방식으로 등록한다.

스프링 컨테이너에 빈을 등록하는 방법은 크게 두 가지가 있다.

1. 컴포넌트 스캔 (Component Scanning)

   - 스프링은 `@Component` 어노테이션이 붙어있는 클래스의 객체를 생성해 빈으로 등록한다.

     기본적으로 실행시키는 메인메서드의 동일 또는 하위 패키지들이 컴포넌트 스캔 대상이다.

   - [웹 애플리케이션 3계층 구조](https://github.com/rlaalstjd00/TIL/blob/master/09_Spring/01_%EA%B3%84%EC%B8%B5%EA%B5%AC%EC%A1%B0.md)에 맞춰 개발하면 `@Controller`, `@Service`, `@Repository` 어노테이션을 쓰는 클래스가 생기는데, 이 세 어노테이션은 모두 내부적으로 `@Component` 어노테이션을 사용하기 때문에 스프링 빈으로 등록이 된다.

   - 등록된 스프링 빈을 주입하기 위해선 `@Autowired` 라는 어노테이션을 사용하는데, 생성자에 `@Autowired` 어노테이션이 있으면 연관된 객체를 스프링 컨테이너에서 찾아 넣어준다.

   ````java
   @Controller
   public class UserController{
       private final MemberService memberService;
       
       @Autowired
       public MemberController(MemberService memberService){
           this.memberService = memberService;
       }
   }
   ````

   > 위의 코드에서 어노테이션을 통해 memberService 를 주입받고 있다.
   >
   > 만약 `MemberService` 클래스에 `@Service` 어노테이션을 쓰지 않으면 스프링 빈에 등록되지 않아 사용할 수 없다는 점을 주의하자.

2. 자바 코드로 직접 등록

   - `SpringConfig` 라는 클래스를 만들어 주고, 그 클래스가 스프링 빈 관리 클래스라는 것을 명시하기 위해 클래스에 `@Configuration` 어노테이션을 붙여준다.
   - 그 클래스 안에 `@Bean` 어노테이션을 사용해 빈을 등록할 수 있다.

   ````java
   @Configuration
   public class SpringConfig{
       @Bean
       public MemberService memberService(){
           // memberRepository 빈을 등록했으므로 여기서도 사용 가능하다.
           return new MemberService(memberRepository());
       }
       
       @Bean
       public MemberRepository memberRepository(){
           // memberRepository는 인터페이스이므로 리턴은 구현체인 DBMemeberRepository로 한다.
           return new DBMemberRepository();
       }
   }
   ````

   > 위의 코드는 빈을 등록해놓은 `SpringConfig` 클래스를 나타낸 것이다.
   >
   > 만약 후에 `DBMemberRepository()` 가 다른 레포지토리로 변경 된다고 해도, 리턴하는 부분만 바꿔주면 되므로 편하다.
   >
   > 이렇게 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 컴포넌트 방식보다는 직접 등록을 해주는 방식이 좋다.

