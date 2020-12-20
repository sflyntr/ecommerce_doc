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
> BillingProfile 은 우선 Cart에서 Checkout page로 이동시에는 해당 profile이 user 기준으로 생성되어야 한다. 즉 장바구니를 결제하는 사람에 대한 정보를 담는 것이 빌링프로파일이다.
>> 추후에 이 정보는 결제PG사의 customer_id와 연결될 것이다.

ModelManager는 BillingProfile에 대한 new_or_get만 추가적으로 만든다.

<br/>
