## HTTP 요청 메시지

HTTP 메시지 바디를 통해 넘어온 데이터는 요청 파라미터와 다르게 `@RequestParam` 이나 `@ModelAttribute` 사용이 불가능하다.

요청 메시지가 단순 텍스트인 경우와 JSON인 경우로 나눠서 살펴보자.

<br>

---

### 단순 텍스트 - InputStream과 Writer

HTTP 바디에 있는 텍스트 데이터를 `InputStream` 을 통해 읽을 수 있다.

```java
@PostMapping("/request-body-string")
public void requestBodyString(InputStream inputStream, Writer responseWriter) throws IOException {

  String messageBody = StreamUtils.copyToString(inputStream, StandardCharsets.UTF_8);
  log.info("messageBody={}", messageBody);
  responseWriter.write("ok");
}
```

스프링 MVC는 `InputStream` 과 `Writer`을 파라미터로 지원하기 때문에, `request` 와 `response` 를 파라미터로 받아서 `InputStream` 과 `Writer`을 꺼내는 과정을 할 필요가 없다.

<br>

### 단순 텍스트 - HttpEntitiy

`HttpEntitiy` 를 이용해서 HTTP 헤더와 바디를 편리하게 조회해올 수 있다.

````java
@PostMapping("/request-body-string")
public HttpEntity<String> requestBodyString(HttpEntity<String> httpEntity){
  String messageBody = httpEntity.getBody();
  log.info("messageBody={}", messageBody);

  return new HttpEntity<>("ok");
}
````

`HttpEntitiy`는 응답에서도 사용 가능하며, 메시지 바디 정보를 직접 반환한다.

<br>

### 단순 텍스트 - @RequestBody

`@RequestBody` 어노테이션을 이용하면 위의 과정보다 훨씬 편하게 메시지 바디를 조회할 수 있다.

````java
@ResponseBody
@PostMapping("/request-body-string")
public String requestBodyString (@RequestBody String messageBody){

  log.info("messageBody={}", messageBody);

  return "ok";
}
````

바디만 조회가 가능하며, 헤더 정보가 필요하다면 `@RequestHeader` 파라미터나 위의 `HttpEntitiy`를 이용하면 된다.

<br>

----

### JSON - @RequestBody

JSON 형식의 데이터도 마찬가지로 `@RequestBody` 어노테이션을 이용하면 직접 만든 객체로 변환해 저장할 수 있다.

````java
@Data
public class HelloData {
    private String username;
    private int age;
}
````

`HelloData` 클래스가 위와 같이 정의되어있다고 가정하자.

````java
@ResponseBody
@PostMapping("/request-body-json")
public String requestBodyJson(@RequestBody HelloData data) {
  log.info("username={}, age={}", data.getUsername(), data.getAge());
  return "ok";
}
````

만약 JSON 데이터를 `{"username":"userA", "age"="20"}` 이라고 보냈다면, 해당 데이터를 `HelloData` 타입의 객체 `data` 로 만들어 저장해주는 것이다.

참고로 반환타입을 `HelloData` 로 지정하고 `return data` 한다면 JSON 형식의 데이터를 직접 반환받을 수도 있다.

<br>

### JSON - HttpEntitiy

앞서 단순 텍스트와 같이 `HttpEntitiy`를 사용해도 된다.

```java
@ResponseBody
@PostMapping("/request-body-json")
public String requestBodyJson(HttpEntity<HelloData> data) {
  HelloData helloData = data.getBody();
  log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());
  return "ok";
}
```



