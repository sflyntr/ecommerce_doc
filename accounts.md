# Model

## GuestEmail
email, active, update, timestamp



# View

## guest_register_view

guest 등록 폼을 제공한다.
그리고 등록을 하게 되면 정식 사용자가 아니므로 다음에 갈 페이지를 지정해야 한다.
post인경우 갈 페이지와 get 인 경우 갈 페이지 둘다 지정한다.

이 다음에 갈 페이지는 request에서 결정해야 한다.
따라서 request의 next key를 받아서 그 값에 해당되는 페이지로 이동시킨다.

form에 값이 있으며 valid하면, GuestEmail 모델객체를 생성하고 그 pk(id)를 session에 set한다.
그리고 is_safe_url이면 redirect한닫.
만약 is_safe_url이 아니면(즉, url이 None이면) "/register/"로 redirect한다.

form이 invalide이면, "/register/"로 redirect한다.

## login_page

**FORM**으로 부터의 View 페이지 처리 일반적인 사항

|기능|요약|
|:---|:---|
|**Form**선언  |해당 페이지에서 사용자가 입력할 **Form**을 보여주기 위함|
|**Next**설정  |**Form**의 값을 처리한 이후 다음에 이동할 redirect url을 설정|
|**Form**처리  |**Form** 데이터 존재시, 또는 미존재시 수행할 기능을 정의|
|**Login**처리 |1. 임시사용자 정보 clear <br> 2. 세션에 사용자정보 담기(django는 login함수 사용)|

- 로그인 이후에 이동될 페이지 정보는 request 로 부터 받는다. ( get, post )  

- 로그인 form 처리  
  1. valid
    - authenticate 함수로 form 에 들어온 정보를 인증한다.(인증정보는 user에 반환된다.)
      1. 인증이 된다면
        - djanog의 login 함수를 호출한따.(즉 인증된 사용자라는 뜻이다.)
        - login 후 session 의 혹시 모를 guest_email_id 가 있다면 삭제한다.
        - next_url로 redirect한다.(is_safe_url확인)
        - 만약 is_safe_url이 아니라면, 로그인 했으니 root("/")로 redirect한다.
      2. 인증이 안된 사용자라면
        - login.html로 로그인Form과 함께 render를 다시 한다.

  2. not valid
    - login.html로 로그인Form과 함께 render를 한다.


## register_page

등록 form 이 valid 인 경우, User를 생성한다.  
등록 form 이 invalide 인 경우, 등록 form과 함께 accounts/register.html 페이지를 render한다.  
