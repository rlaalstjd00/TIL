## Request Mapping

Request Mapping을 보기 앞서`@Controller`와 `@RestController`의 차이에 대해 간단히 짚고 넘어가자. 

- `@Controller`는 반환 타입이 `String` 이라면, 해당 문자열을 이름으로 가지는 뷰를 찾아 랜더링한다.
- `@RestController`는 뷰의 이름을 찾는 것이 아니라, 바로 HTTP 메시지 바디에 입력된다.
- `@Controller`로 사용해도 메서드 범위에 `@ResponseBody` 어노테이션을 적으면 그 메서드에 한해 반환된 문자열이 HTTP 메시지 바디에 입력된다.



### @RequestMapping

`@RequestMapping` 어노테이션은 메서드 단위에 사용할 시, 특정 URL 호출이 오면 해당 메서드를 실행하게 매핑 해주는 역할을 한다.

````java
@Slf4j
@RestController
public class MappingController{
  @RequestMapping("/hello-spring")
  public String helloSpring(){
    log.info("helloSpring");
    return "ok";
  }
}
````

이 때 별도의 설정을 하지 않으면 HTTP 메서드에 상관없이 모두 전송되므로 `@RequestMapping(value = "/hello-spring", method=RequestMethod.GET)` 과 같이 설정을 해줘야한다. 메서드마다 모두 전송 방식이 다른데 그 때마다 저렇게 쓰긴 너무 길기 때문에 `@GetMapping("/hello-spring")` 같은 어노테이션도 지원한다.



아래의 예시부터는 클래스범위는 생략하며 클래스 단위에 `@Slf4j` 와 `@RestController`가 있다고 전제한다.

### 경로변수 사용

`@PathVariable` 이라는 어노테이션을 이용해 경로변수를 사용할 수 있다.

````java
@GetMapping("/mapping/{userId}")
public String mappingPath(@PathVariable("userId") String userId){
  log.info("userId={}", userId);
  return "ok";
}
````

위처럼 쓰면 매칭되는 부분을 편리하게 조회할 수 있다.

예를 들어 URL이 `localhost:8080/mapping/userA` 로 들어왔다면 로그는 `userId=userA` 로 출력되는 것이다.

경로변수는 여러개도 사용 가능하며, `@PathVariable` 이름과 파라미터 이름이 같으면 `@PathVariable String userId` 와 같이 생략가능하다.



### 파라미터 추가 매핑 

특정 파라미터의 유무 조건을 추가할 수 있다.

````java
@GetMapping(value = "/mapping-param", params = "mode=debug")
public String mappingParam(){
  log.info("mappingParam");
  return "ok";
}
````

쿼리 파라미터에 `mode=debug` 가 있을때만 호출된다.



### 헤더 추가 매핑

특정 헤더의 유무 조건을 추가할 수 있다.

````java
@GetMapping(value = "/mapping-header", headers = "mode=debug")
public String mappingHeader(){
  log.info("mappingHeader");
  return "ok";
}
````

HTTP 헤더에 `mode=debug` 가 있을때만 호출된다.



### 미디어타입 조건 매핑 Content-Type, consume

HTTP `Content-Type` 헤더로 매핑한다.

````java
@PostMapping(value = "/mapping-consume", consumes = "application/json")
public String mappingConsumes(){
  log.info("mappingConsume");
  return "ok";
}
````

`Content-Type`이 `application/json` 일때만 호출된다.



### 미디어타입 조건 매핑 Accept, produce

HTTP `Accept` 헤더로 매핑한다.

````java
@PostMapping(value = "/mapping-produce", produces = "text/html")
public String mappingProduce(){
  log.info("mappingProduce");
  return "ok";
}
````

`Accept` 가 `text/html` 일때만 호출된다.