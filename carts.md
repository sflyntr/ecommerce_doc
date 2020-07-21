# Model

### Carts

> 카트는 장바구니이다. 누가 담았는지 알아야 하므로 user정보가 필요하다. 게스트도 cart에 담을수 있어야 하니 null=True임.
> 그리고 상품정보도 있어야 한다. 하나의 cart에 여러개의 상품이 담겨야 하며, 또한 하나의 상품이 여러 cart에도 담겨야 한다.
> 상품필드는 product이 없을수도 있다. 즉 cart에 넣었다가 다 빼는 경우 빈카트만 남게 되는 것이다.
> 게스트도 상품을 담기때문에 user정보는 없을수 있다. 그럼 게스트의 경우는 카트를 생성한 후 cart_id(PK)를 세션에 가지고 다니어야 한다.
> subtotal은 상품금액 SUM 이며 total은 상품금액 SUM에 일정금액을 추가한 전체 총액이다.

> 참고로 ManyToMany관계의 필드는 실제 물리 필드가 생성되지 않고, 중간테이블(매핑)이 자동으로 생성된다.

|이름|요약|
|:---|:---|
|**user**  |사용자정보 User의 외래키(User는 장고모델임)|
|**products**  |products|
|**subtotal**  |상품금액에 대한 총액|
|**total**  |subtotal에 부가세등 일부금액 추가해서 전체주문금액|
|**update**  |수정일시|
|**timestamp**  |등록일시|

> 여기에도 Trigger(Signal)은 있다.
>> 카트의 Product 정보가 변경(m2m_changed)되는 경우, 그 변경은 실제 상품이 추가된 후 또는 상품이 삭제된 후 또는 전체가 삭제된 후에 처리하는데,
>> total 과 subtotal을 변경한다.
>> 카트가 저장되는 경우에는 저장전에(pre_save) 최총 subtotal로 total을 재계산해서 넣는다.

<br/>
