# Model

### GuestEmail

> GuestEmail 모델은 일반 사용자가 아닌 손님으로 체크아웃을 할때 사용하며, 이메일을 주요정보로 한다.

|이름|요약|
|:---|:---|
|**email**  |게스트의 이메일정보|
|**active**  |현재 사용 여부(active)|
|**update**  |수정일시|
|**timestamp**  |등록일시|

### User

> 이 클래스는 django에서 제공하는 User를 대신할 User Class이다.

|이름|요약|
|:---|:---|
|**email**  |게스트의 이메일정보|
|**active**  |현재 사용 여부(active)|
|**staff**|스태프여부|
|**admin**|어드민여부|
|**timestamp**  |등록일시|



<br/>

# View

### guest_register_view

> 손님으로 등록하기 위한 view 정보이다. 손님등록할 form을 보여준다.

|기능|요약|
|:---|:---|
|**Form**선언  |해당 페이지에서 사용자가 입력할 **Form**을 보여주기 위함|
|**Next**설정  |**Form**의 값을 처리한 이후 다음에 이동할 redirect url을 설정|
|**Form**처리  |**Form** 데이터 존재시, 또는 미존재시 수행할 기능을 정의|
|**게스트**처리  |1. 게스트정보 생성 성공시 해당 정보의 pk(id)를 세션에 담는다. <br>2. 오류나 비정상 url등 발생시엔 항상 다시 등록페이지로 이동한다.(register페이지)|


### login_page

> 사용자가 로그인을 하기 위한 view 이다.

|기능|요약|
|:---|:---|
|**Form**선언  |해당 페이지에서 사용자가 입력할 **Form**을 보여주기 위함|
|**Next**설정  |**Form**의 값을 처리한 이후 다음에 이동할 redirect url을 설정|
|**Form**처리  |**Form** 데이터 존재시, 또는 미존재시 수행할 기능을 정의|
|**Login**처리 |1. 임시사용자 정보 clear <br> 2. 세션에 사용자정보 담기(django는 login함수 사용)|

### register_page

> 신규 사용자를 등록하기 위한 view이다.

|기능|요약|
|:---|:---|
|**Form**선언  |해당 페이지에서 사용자가 입력할 **Form**을 보여주기 위함|
|**Next**설정  |**Form**의 값을 처리한 이후 다음에 이동할 redirect url을 설정|
|**Form**처리  |**Form** 데이터 존재시, 또는 미존재시 수행할 기능을 정의|
|**등록**처리  |1. 사용자 모델은 django의 User 모델을 사용하도록 한다.|

<br/>

# Form

### GuestForm

> Guest를 등록하기 위한 Form 이다.

|이름|요약|
|:---|:---|
|**email**  |게스트의 이메일정보|
|**active**  |현재 사용 여부(active)|
|**update**  |수정일시|
|**timestamp**  |등록일시|

### LoginForm

> 사용자 로그인을 하기 위한 Form이다.

|이름|요약|
|:---|:---|
|**username**  |사용자아이디|
|**password**  |비밀번호|

### RegisterForm

> 사용자 로그인을 하기 위한 Form이다.

|이름|요약|검증|
|:---|:---|:---|
|**username**  |사용자아이디|이미 존재하는지 여부|
|**email**  |사용자의 이메일정보|이미 존재하는지 여부|
|**password**  |비밀번호|
|**password2**  |확인용 비밀번호|

`Form 검증 : password와 password2 가 일치하는지 여부`
