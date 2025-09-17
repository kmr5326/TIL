### spring validation
@NotNotBlank, @Valid

validation 예외 발생하면 BindingResult 객체에 오류가 담겨져 들어온다.
```java
List<FieldError> fieldErrors = bindingResult.getFieldErrors();
        if(fieldErrors.size() > 0) {
            for (FieldError fieldError : bindingResult.getFieldErrors()) {
                log.error(fieldError.getField() + " 필드 : " + fieldError.getDefaultMessage());
            }
            return "redirect:/api/user/signup";
        }
```

### RestTemplate
동기식 HTTP 클라이언트

### WebClient
비동기+논블로킹(리액터 기반) HTTP 클라이언트

### 영속성 컨텍스트
1차 캐시, 쓰기 지연 저장소, 변경 감지

### 지연 로딩 n+1 문제
fetch join을 통해 방지