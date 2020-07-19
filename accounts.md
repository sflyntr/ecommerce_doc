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

## register_page

등록 form 이 valid 인 경우, User를 생성한다.  
등록 form 이 invalide 인 경우, 등록 form과 함께 accounts/register.html 페이지를 render한다.  
