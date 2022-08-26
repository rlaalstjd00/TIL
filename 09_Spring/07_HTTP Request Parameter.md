## HTTP 요청 파라미터

`GET` 방식의 쿼리 파라미터 전송이나, HTML `form` 태그를 이용한 `POST` 방식의 전송은 둘다 형식이 같다. 따라서 이러한 요청 파라미터를 조회할 수 있는 방법을 알아보자.

아래의 예제코드는 모두 메서드 단위로, 클래스 범위에 모두 `@Slf4j`와 `@RestController`가 있다고 전제한다.

<br>

### @RequestParam의 사용

````java
@RequestMapping("/request-param")
public String requestParam(
  @RequestParam String username,
  @RequestParam int age) {

  log.info("username={}, age={}", username, age);
  return "ok";
}
````

`@RequestParam` 어노테이션을 이용하면 파라미터를 편리하게 받아올 수 있다.

자료형 변환도 자동으로 해주기 때문에, `request.getParameter("username")` 이나 `Integer.parseInt(request.getParameter("age"))` 같이 불편하게 할 필요가 없어지는 것이다.

참고로, `String`, `int`, `Integer` 같은 단순 타입이면 `@RequestParam` 어노테이션도 생략이 가능하다.

<br>

### @ReqeustParam 파라미터의 필수 여부

````java
@RequestMapping("/request-param")
public String requestParam(
  @RequestParam String username,
  @RequestParam(required = false) Integer age) {
  
  log.info("username={}, age={}", username, age);
  return "ok";
}
````

`@RequestParam` 어노테이션은 `required` 속성으로 파라미터의 필수 여부도 설정해줄 수 있다. 기본값은 필수, 즉 `true` 이며 필수가 아닌 선택으로 바꾸고 싶다면 명시적으로 `false` 로 바꿔주면 된다.

> 왜 여기서 `age`는 `int`가 아니라 `Integer`일까?
>
> - `age`의 필수 속성은 `false`로 값이 안들어올 수가 있기 때문이다. 이 때는 `null`이 할당되며, 이를 받을 수 있는 `Integer` 타입으로 설정하는 것이다.
>
> **`@RequestParam` 어노테이션을 생략하면 `required = false`가 됨에 주의하자!!**

<br>

### @RequestParam 파라미터의 기본값

````java
@RequestMapping("/request-param")
public String requestParam(
  @RequestParam(defaultValue = "guest") String username,
  @RequestParam(defaultValue = "-1") int age) {
  log.info("username={}, age={}", username, age);
  return "ok";
}
````

위처럼 기본값도 설정이 가능한데, 이는 값이 들어오지 않으면 설정한 기본값으로 할당되는 것이다. 이 때는 `age`의 기본값을 -1로 설정했으므로 `int` 타입으로 받을 수 있는 것이다.

> *참고*
>
> `required = true` 속성으로 설정한 파라미터는 빈 문자열, 즉 `userId=` 같은 파라미터도 받아진다.
>
> 하지만 `defaultValue` 속성으로 기본값을 설정해주면 빈 문자열도 기본값으로 바뀐다.

<br>

### @RequestParam 파라미터 Map으로 조회

````java
@RequestMapping("/request-param")
public String requestParam(@RequestParam Map<String, Object> paramMap){
  log.info("username={}, age={}", paramMap.get("username"), paramMap.get("age"));
  return "ok";
}
````

파라미터를 `Map` 형식으로도 받을 수 있다. 같은 `key` 값에 대해 파라미터의 값이 하나라면 `Map`으로, 둘 이상이라면 `MultiValueMap`을 사용한다.

> - `Map` : `key = value`
> - `MultiValueMap` : `key = [value1, value2, value3, ..]`

<br>

### @ModelAttribute의 사용

받아온 파라미터를 객체에 넣어 활용하기 위해 `MyData` 클래스를 하나 만들었다고 가정하자.

````java
@Data
public class MyData{
  private String username;
  private int age;
}
````

파라미터로 받아온 데이터를 객체로 활용하기 위해서는

````java
// 파라미터로 username, age를 받았다고 가정
MyData myData = new MyData();

data.set(username);
data.set(age);
````

위의 과정을 거쳐야 할 것이다. 다뤄야할 데이터가 많아지면 굉장히 번거로운 과정인데, 이를 모두 자동화 해주는 것이 `@ModelAttribute` 어노테이션이다.

````java
@RequestMapping("/model-attribute")
public String modelAttribute(@ModelAttribute MyData myData){
  log.info("username={}, age={}", myData.getUsername(), myData.getAge());
  return "ok";
}
````

위의 코드에서, `@ModelAttribute` 어노테이션은 `MyData` 객체를 생성한 후 해당 객체의 프로퍼티를 `setter`를 이용해서 파라미터의 값을 모두 할당해준다.

`@ModelAttribute`는 생략도 가능하다.

> `@RequestParam` 과 `@ModelAttribute` 두 어노테이션 모두 생략이 가능한데, 어떻게 구별해서 사용하는 것일까?
>
> - `String`, `int`, `Integer` 같은 단순 타입이면 `@RequestParam`
> - 나머지 (직접 만든 객체도 포함) 는 모두 `@ModelAttribute` (argument resorver로 지정해둔 타입은 제외)