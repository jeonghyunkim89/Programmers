## [NCS전공교과] 요구사항 확인 (문제해결시나리오) 1회차
다음과 같은 상황이 발생하는 원인과 조치내용에 대해서 보고서 작성 후 제출하시오.<br>
다음은 로그인여부를 체크하기 위한 Interceptor 및 Interceptor설정파일을 작성하였으나 정상적으로 동작하지 않았다.<br>
다음 조건 및 소스코드를 분석하여 원인을 파악하고 조치사항을 작성하시오.<br><br>

## [조건]
```
1. 로그인 상태 확인

- 로그인이 되어있으면 session에 "user"를 키값으로하여 UserDTO타입의 데이터로 회원정보가 저장되어 있다.

2. 로그인이 처리되어있어야 하는 기능

- 마이페이지, 정보수정, 회원탈퇴, 전체회원 조회

3. 로그인이 되어있지 않은 상태로 로그인이 처리되어 있어야 하는 기능을 접근하는 경우

- 해당 컨트롤러로 접근하지 않고, 메인페이지로 이동시킨다.

※ 컨트롤러의 소스코드는 생략되어있다.
```

## [소스코드]
```
[UserController.java]

@Controller

@RequestMapping(value="/user")

public class UserController {

@GetMapping(value="/login")

public String login() {

//로그인

}

@GetMapping(value="/allUser")

public String allUser() {

//전체회원조회

}

@PostMapping(value="/regist")

public String regist() {

//회원가입

}

@GetMapping(value="/mypage")

public String mypage() {

//마이페이지

}

@PostMapping(value="/modify")

public String modify() {

//정보수정

}

@GetMapping(value="/remove")

public String remove() {

//회원탈퇴

}

}
```
```
[LoginInterceptor.java]

public class LoginInterceptor implements HandlerInterceptor{

@Override

public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)

throws Exception {

HttpSession session = request.getSession();

UserDTO u = (UserDTO)session.getAttribute("u");

if(u == null) {

return true;

}else {

return false;

}

}

}
```
```
[WebConfig.java]

@Configuration

@EnableWebMvc

public class WebConfig implements WebMvcConfigurer{

@Override

public void addInterceptors(InterceptorRegistry registry) {

registry.addInterceptor(new LoginInterceptor())

.addPathPatterns("/user/mypage","/user/modify","/user/remove");

}

}
```
## 나의 문제풀이(원인)
```
원인 1. preHandle 메소드에서 현재 세션에 UserDTO 객체가 존재하는지
        확인하는 과정에서 문제가 있다.
        UserDTO u = (UserDTO)session.getAttribute("u"); 

원인 2. if(u  == null) { return true; } else { return false;} 에서
       로그인 여부를 확인하는 코드가 반대로 되어 있다.
       로그인유저가 null이 아닐때 true를 반환하게 코드를 수정해야한다.​

원인 3. addPathPatterns에서 로그인 여부를 체크하는 페이지
       (마이페이지, 정보수정, 회원탈퇴)에 대해서만
        인터셉터가 동작하도록 설정되어 있다.
```
## 나의 문제풀이(조치내용)
```
원인1 - 조치내용 : UserDTO u = (UserDTO)session.getAttribute("user");


원인2 - 조치내용 : if (u != null) {

                        return true;

                } else {

                        response.sendRedirect(request.getContextPath());

                        return false;

                }​

원인3 - 조치내용 : registry.addInterceptor(new LoginInterceptor())

                  .addPathPatterns("/user/mypage", "/user/modify",
                  
                  "/user/remove", "/user/allUser");​
```
## 모범답안(원인)
```
나의 문제풀이(원인)2번에서 로그인이 되어있지 않은 상태로
로그인이 처리되어 있어야 하는 기능을 접근하는 경우
해당 컨트롤러로 접근하지 않고, 메인페이지로 이동시키는 [조건]3번을 추가했어야 한다.
```