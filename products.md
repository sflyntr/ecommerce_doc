# Model

## Product

> Product는 상품이다. 따라서 기본적으로 상품제목/요약/상세설명/가격은 필수이다.  
> 그리고 쇼핑몰이니 상품그램이 있어야 한다.  
> 부가적으로 주요상품여부, 활성상태여부, 등록일시 등이 필요하다.  

|이름|요약|
|:---|:---|
|**title**  |상품제목|
|**slug**  |슬러그.상품요약|
|**description**  |상품설명|
|**price**  |상품가격|
|**image**  |상품이미지|
|**featured**  |주요상품여부|
|**active**  |활성상태여부|
|**timestamp**  |등록일시|

> Model class ( 5가지를 기본으로 한다. )  
>> 모델의 속성정의  
>> 모델을 관리할 모델관리자 정의( 기본은 **objects** 변수에 있다. )  
>> 모델에 접근하는 absolute_url 정의  
>> getter  
>> __str__  

### QuerySet : ProductQuerySet  
model.query.QuerySet을 상속한다.  

### ModelManager : ProductManager  
model.ModelManager를 상속해야 한다.    
가장 중요한것은 get_queryset을 재정의 하는 기능을 한다.    
굳이 재정의 할 필요가 없다면 안해도 된다.    
그리고 필요한 queyrset 함수들을 만들면 된다.   

### functions  
get_file_name(filepath) -> name, ext : 화일경로가 포함된 화일명이 들어오면 순수화일명과 확장자를 return한다.  
upload_image_path(filename) -> new_file_name : 실제 사용자가 화면에서 이미지를 업로드하면 화일명을 중복이 나지 않게 랜덤하게 생성한다.  

> 여기에도 Trigger(Signal)은 있다.
>> 카트의 Product 정보가 변경(m2m_changed)되는 경우, 그 변경은 실제 상품이 추가된 후 또는 상품이 삭제된 후 또는 전체가 삭제된 후에 처리하는데,
>> total 과 subtotal을 변경한다.
>> 카트가 저장되는 경우에는 저장전에(pre_save) 최총 subtotal로 total을 재계산해서 넣는다.


## utils.py
product 의 slug 를 만들기 위한 util 함수를 만든다.
- random_string_generator 는 길이와 랜덤을 만들기 위한 스트링을 받아서 길이만큼 랜덤스트링을 만든다.  
- unique_slug_generator 는 객체와 new_slug를 받는다. 
  - new_slug가 들어오면 이것이 원래 존재하는건지 확인하고 존재하면 새로만든다.(인스턴스명-랜덤스트링4자리)
  - new_slug각 안들어오면 instance로 부터 slugify학고 그 뒤에 랜덤스트링4자리를 붙여 만든다.
  

<br/>

# View

### Carts

> 카트 관련 View는 일단 장바구니 담기 하면 이동되는 페이지 그리고 이미 담겨있는게 뭔지 보는 페이지 사실 이 2개는 같은 곳을 볼것이다.
> 그 위치에서 장바구니에 상품을 변경하면 이동되는 페이지. 이것도 같은 것일것이다.
> 결국 View에 기능들이 있지만, 이동되는 최종 위치는 cart_home.html일것 

|이름|요약|
|:---|:---|
|**cart_home**  |cart_home.html을 render하는 것인떼, 이 페이지에는 카트이므로 카트정보가 있어야 한다.|
|**cart_update**  |장바구니 담기할때 cart정보가 update되어야 하는 로직이다. 즉, 상품정보가 request에 있으며, 약간 트릭인데 있으면 지우고, 없으면 넣는다. <br/> 그리고 상단에 상품갯수도 보여야한다.|
|**checkout_home**  |checkout.html로 이동한다. 여기서 중요한 것은 checkout페이지에서 보여줄 내용은 billing_profile의 존재여부로 로그인/게스트로그인을 보여주거나 아니면 실제 페이지를 보여준다. |

> 자주 사용하는 기능이 cart를 생성하는 것이니, cart_create함수를 따로 만들자.user가지고 만드는거다.


<br/>
