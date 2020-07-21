# Model

### BillingProfile

> BillingProfile 체크아웃시 사용하는 청구프로파일 정보이다.

|이름|요약|
|:---|:---|
|**user**  |사용자정보 User와 1대1관계(User는 장고모델임)|
|**email**  |이메일|
|**active**  |사용여부|
|**update**  |수정일시|
|**timestamp**  |등록일시|

> BillingProfile 정보는 기본적으로 정식 사용자는 User객체가 신규로 생기면 그 이후(post_save) 자동으로 생성된 User객체를 받아서 instance로는 그 객체, 이메일로 그 객체의 email를 채워서 BillingProfile이 생긴다.

<br/>
