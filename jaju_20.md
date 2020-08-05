# Wisetracker Integration Guide

와이즈트래커 2.0을 'JAJU' 앱에 연동하기 위한 내용을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.



> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [SDK 적용](./jaju_20.md#SDK-적용)
* [회원가입 측정](./jaju_20.md#회원가입-측정)
* [JAJU클럽 가입 측정](./jaju_20.md#JAJU클럽-가입-측정)
* [로그인 측정](./jaju_20.md#로그인-측정)
* [검색 측정](./jaju_20.md#검색-측정)
* [상품 조회 측정](./jaju_20.md#상품-조회-측정)
* [상품 리뷰 조회 측정](./jaju_20.md#상품-리뷰-조회-측정)
* [상품 공유하기 측정](./jaju_20.md#상품-공유하기-측정)
* [위시리스트에 담기 측정](./jaju_20.md#위시리스트에-담기-측정)
* [장바구니 담기 측정](./jaju_20.md#장바구니-담기-측정)
* [구매 완료 측정](./jaju_20.md#구매-완료-측정)
* [개별 화면 조회 측정](./jaju_20.md#개별-화면-조회-측정)
* [장바구니 조회 측정](./jaju_20.md#장바구니-조회-측정)
* [카테고리 화면 조회 측정](./jaju_20.md#카테고리-화면-조회-측정)
* [기획전 조회 측정](./jaju_20.md#기획전-조회-측정)
* [기획전 공유하기 측정](./jaju_20.md#기획전-공유하기-측정)
* [App Push 동의 여부 측정](./jaju_20.md#App-Push-동의-여부-측정)
* [적용 후 데이터 검증](./jaju_20.md#적용-후-데이터-검증)
  * [AOS](./jaju_20.md#AOS)
  * [iOS](./jaju_20.md#iOS)



## SDK 적용

아래 링크를 참고하여 앱에 와이즈트래커 2.0 SDK를 적용해주세요.

* [Android](http://document.wisetracker.co.kr/v2/docs/sdk/android/android-install-guide)
* [iOS](http://document.wisetracker.co.kr/v2/docs/sdk/ios/ios-install-guide)



## 회원가입 측정

회원가입 횟수를 측정하기 위해 **가입 완료 화면 내**에 API를 적용합니다.



### 측정 API

```html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_signup_complete";
	DOT.logEvent(event);
</script>
```



## JAJU클럽 가입 측정

유저가 JAJU클럽으로 가입한 횟수를 측정하기 위해 **클럽 가입이 완료된 시점**에 API를 적용합니다. 아래 세 가지 경우에 모두 적용되어야 합니다.

1. 회원가입 프로세스에서 '자주클럽'에 체크 표시를 한 경우
2. 마이페이지 > 관심클럽에서 자주클럽에 가입한 경우
3. 앱 내 팝업을 통해 자주클럽에 가입한 경우



### 측정 API & 적용예시

``` javascript
function joinJajuClub() {
	...
	alert("자주클럽에 가입 되었습니다.");
	var event = new Object();
	event["event"] = "signup_jajuclub";
	event["g102"] = 1;
	DOT.logEvent(event);
}
```



## 로그인 측정

로그인 횟수와 유저 정보를 측정하기 위해 **로그인 완료 시점**에 API를 적용합니다. 아래에 리스팅된 정보는 반드시 매핑 테이블을 참고하여 적용해 주시기 바랍니다.

1. 회원 성별
2. 회원 연령대 (5세 기준)
3. 회원 유형 - 일반 회원 / 임직원 구분
4. 회원 등급 - SI 멤버십 등급에 따른 구분
5. JAJU클럽 등급
6. 회원 연령 (1세 기준)
7. 마케팅 앱푸시 동의 여부



### 매핑 테이블

#### 성별

| 성별                                   | genderCode    |
| -------------------------------------- | ------------- |
| 남성                                   | male          |
| 여성                                   | female        |
| 기타 (남성 또는 여성이 아닌 모든 경우) | non_avaliable |



#### 연령대

| 연령대      | ageCode   |
| ----------- | --------- |
| 10세 미만   | under_10s |
| 10세 - 19세 | 10-19     |
| 20세 - 24세 | 20-24     |
| 25세 - 29세 | 25-29     |
| 30세 - 34세 | 30-34     |
| 35세 - 39세 | 35-39     |
| 40세 - 44세 | 40-44     |
| 45세 - 49세 | 45-49     |
| 50세 - 54세 | 50-54     |
| 55세 - 59세 | 55-59     |
| 60세 이상   | over_60s  |



#### 회원 유형

| 회원 유형 | attr1Code |
| --------- | --------- |
| 일반 회원 | member    |
| 임직원    | staff     |



#### 회원 등급

| 회원 등급 | attr2Code |
| --------- | --------- |
| Bronze    | bronze    |
| Silver    | silver    |
| Gold      | gold      |
| Platinum  | platinum  |
| Diamond   | diamond   |



#### JAJU클럽 등급

| JAJU클럽 등급 | attr3Code |
| ------------- | --------- |
| White         | white    |
| Gray          | gray    |
| Black         | black      |



#### App Push 동의 여부

| 동의 여부 | attr5Code |
| --------- | --------- |
| 동의      | opt-in    |
| 비동의    | opt-out   |



#### 로그인 타입

| 로그인 타입         | loginTp  |
| ------------------- | -------- |
| 신세계인터내셔날 ID | id       |
| 카카오              | kakao    |
| 네이버              | naver    |
| 페이스북            | facebook |



### 측정 API

```javascript
DOT.setUser(User.setGender("${genderCode}")
	.setAge("${ageCode}")
	.setAttr1("${attr1Code}")
	.setAttr2("${attr2Code}")
	.setAttr3("${attr3Code}")
    .setAttr4("${유저의실제연령}")
    .setAttr5("${attr5Code}"));
	// 매핑 테이블을 참고하여 치환

var event = new Object();
event["event"] = "w_login_complete";
event["loginTp"] = "${loginTp}"; // 매핑 테이블을 참고하여 치환
DOT.logEvent(event);
```



### 적용예시

Gold 등급의 31세 여성이며, 임직원이 아니며, JAJU클럽 Black 등급이며 App Push 수신에 동의한 회원이 카카오 계정으로 로그인한 경우, 로그인 완료 시점에 아래와 같이 적용

```javascript
DOT.setUser(User.setGender("female")
	.setAge("30-34")
	.setAttr1("member")
	.setAttr2("gold")
    .setAttr3("black")
    .setAttr4("31")
	.setAttr3("opt-in"));

var event = new Object();
event["event"] = "w_login_complete";
event["loginTp"] = "kakao";
DOT.logEvent(event);
```



## 검색 측정

유저의 *검색 방법* 과 *검색어*를 측정하기 위해 **검색 완료 화면에 API를 적용**합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_search";
	event["search_term"] = "${searchTerm}";
	// 검색된 키워드로 치환
	event["g20"] = ${numberOfResults}; // integer
	// 검색 결과로 출력된 '상품 item'의 개수 (기획전, JAJU LIVE 제외)
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 "선풍기"를 검색한 경우 **검색 완료 화면**에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_search";
	event["search_term"] = "선풍기";
	event["g20"] = 4;
	DOT.logEvent(event);
</script>
```



## 상품 조회 측정

개별 상품의 조회수를 측정하기 위해 **상품 상세 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_product";
	screen["page_id"] = "product";
	
	var product = new Object();
	product["product_id"] = "${productId}";
	product["product_name"] = "${productName}";
	product["brand_name"] = "${brandCode}";
	product["category_id_a"] = "${categoryIdA}";
	product["category_name_a"] = "${categoryNameA}";
	product["category_id_b"] = "${categoryIdB}";
	product["category_name_b"] = "${categoryNameB}";
	product["category_id_c"] = "${categoryIdC}";
	product["category_name_c"] = "${categoryNameC}";
	// 조회된 상품의 코드, 명칭, 브랜드코드, 카테고리 대-중-소 정보로 치환
	
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



### 적용예시

*필터를 바꿔쓰는 수압 센 샤워헤드_실버* 상품이 조회된 경우 해당 페이지 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_product";
	screen["page_id"] = "product";
	var product = new Object();
	product["product_id"] = "01P0000237409";
	product["product_name"] = "필터를 바꿔쓰는 수압 센 샤워헤드_실버";
	product["brand_name"] = "J1";
	product["category_id_a"] = "010000000010";
	product["category_name_a"] = "욕실";
	product["category_id_b"] = "010000000104";
	product["category_name_b"] = "욕실소품";
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



## 상품 리뷰 조회 측정

각 상품별로 리뷰 조회수를 측정하기 위해 API를 적용합니다. 아래 설명을 참고하여 API를 적용해 주시기 바랍니다.

* 리스트 화면에 있는 리뷰 버튼을 클릭하여 리뷰를 조회할 수 있습니다.
* 상품 상세화면에 있는 상품 리뷰 탭을 클릭하여 리뷰를 조회할 수 있습니다.
* **위 두 경우 모두 측정할 수 있는 환경**에 API를 적용해 주세요. (예를 들어 버튼 또는 탭 클릭 시점, 또는 리뷰 레이어 내)



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_see_review";
	var product = new Object();
	product["product_id"] = "${productId}";
	product["product_name"] = "${productName}";
	product["brand_name"] = "${brandCode}";
	// 리뷰가 조회된 상품의 코드, 명칭, 브랜드코드로 치환
	event["product"] = product;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *바꿔쓰는 필터 3입* 상품 상세화면에서 리뷰 탭을 클릭한 경우 아래와 같이 적용

``` javascript
var event = new Object();
event["event"] = "w_see_review";
var product = new Object();
product["product_id"] = "01P0000237407";
product["product_name"] = "바꿔쓰는 필터 3입";
product["brand_name"] = "J1";
event["product"] = product;
DOT.logEvent(event);
```



## 상품 공유하기 측정

상품 상세 화면에 있는 공유하기 버튼의 클릭수를 측정하기 위해 **해당 버튼이 클릭된 시점**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "w_share";
	event["share_type"] = "product";
	var product = new Object();
	product["product_id"] = "${productId}";
	product["product_name"] = "${productName}";
	product["brand_name"] = "${brandCode}";
	// 상품코드 상품명 브랜드코드로 치환
	event["product"] = product;
	DOT.logEvent(event);
</script>
```



### 적용예시

*마스터 다용도 삼각 집게* 상품의 **공유버튼이 클릭**된 시점에 아래와 같이 적용

``` javascript
function productShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "product";
    var product = new Object();
	product["product_id"] = "01P0000020576";
	product["product_name"] = "마스터 다용도 삼각 집게";
	product["brand_name"] = "J1";
    event["product"] = product;
	DOT.logEvent(event);
}

onclick="productShare()"
```



## 위시리스트에 담기 측정

상품이 위시리스트에 추가된 횟수를 측정하기 위해 API를 적용합니다. 아래와 같은 경우에 모두 적용되어야 합니다.

* 리스트 화면에 배치된 상품 이미지의 '하트' 클릭
* 상품 상세 하단 Bar에 있는 '하트' 클릭
* 쇼핑백 화면 내의 위시리스트 버튼 클릭



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_add_to_wishlist";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandCode}";
	// 위시리스트에 추가된 상품의 코드, 명칭, 브랜드코드로 치환
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandCode}";
	// 위시리스트에 추가된 상품의 코드, 명칭, 브랜드코드로 치환
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	event["product"] = productArray;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *안전 면봉_80P* 상품을 위시리스트에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
    var event = new Object();
    event["event"] = "w_add_to_wishlist";
    var product1 = new Object();
	product1["product_id"] = "01P0000256908";
	product1["product_name"] = "안전 면봉_80P";
	product1["brand_name"] = "J1";
    event["product"] = product1;
	DOT.logEvent(event);
}
```



유저가 *안전 면봉_80P* 상품과 *전신 스트레칭 폼 롤러 90cm* 상품을 위시리스트에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_wishlist";
    var product1 = new Object();
	product1["product_id"] = "01P0000256908";
	product1["product_name"] = "안전 면봉_80P";
	product1["brand_name"] = "J1";
    var product2 = new Object();
	product2["product_id"] = "01P0000281899";
	product2["product_name"] = "전신 스트레칭 폼 롤러 90cm";
	product2["brand_name"] = "J1";
    var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
    event["product"] = productArray;
	DOT.logEvent(event);
}
```



## 장바구니 담기 측정

상품이 장바구니에 추가된 횟수를 측정하기 위해 상품이 장바구니에 정상적으로 추가된 시점에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_add_to_cart";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandCode}";
	// 장바구니에 추가된 상품의 코드, 명칭, 브랜드코드로 치환
	product1["quantity"] = ${quantity}; // intiger
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandCode}";
	// 장바구니에 추가된 상품의 코드, 명칭, 브랜드코드로 치환
	product1["quantity"] = ${quantity}; // intiger
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	event["product"] = productArray;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *안전 면봉_80P* 상품 2개를 장바구니에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_cart";
    var product1 = new Object();
	product1["product_id"] = "01P0000256908";
	product1["product_name"] = "안전 면봉_80P";
	product1["brand_name"] = "J1";
    product1["qunatity"] = 2;
    event["product"] = product1;
	DOT.logEvent(event);
}
```



유저가 *안전 면봉_80P* 상품 2개와 *전신 스트레칭 폼 롤러 90cm* 상품 1개를 장바구니에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_cart";
    var product1 = new Object();
	product1["product_id"] = "01P0000256908";
	product1["product_name"] = "안전 면봉_80P";
	product1["brand_name"] = "J1";
    product1["qunatity"] = 2;
    var product2 = new Object();
	product2["product_id"] = "01P0000281899";
	product2["product_name"] = "전신 스트레칭 폼 롤러 90cm";
	product2["brand_name"] = "J1";
    product2["qunatity"] = 1;
    var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
    event["product"] = productArray;
	DOT.logEvent(event);
}
```



## 구매 완료 측정

구매 완료 횟수와 매출 관련 데이터를 측정하기 위해 **구매 완료 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object();
	purchase["transaction_id"] = "${transactionId}";
	purchase["currency"] = "${currency}";
	// 구매건의 주문번호와 결제된 화폐의 통화코드로 치환, 원화는 통화코드로 KRW 사용
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandName}";
	product1["category_id_a"] = "${categoryIdA}";
	product1["category_name_a"] = "${categoryNameA}";
	product1["category_id_b"] = "${categoryIdB}";
	product1["category_name_b"] = "${categoryNameB}";
	product1["category_id_c"] = "${categoryIdC}";
	product1["category_name_c"] = "${categoryNameC}";
	product1["quantity"] = ${quantity}; // intiger
	product1["revenue"] = ${revenue}; // intiger
	// 구매된 상품의 코드, 명칭, 브랜드명, 카테고리 대-중-소, 수량, 매출액으로 치환
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	product2["category_id_a"] = "${categoryIdA}";
	product2["category_name_a"] = "${categoryNameA}";
	product2["category_id_b"] = "${categoryIdB}";
	product2["category_name_b"] = "${categoryNameB}";
	product2["category_id_c"] = "${categoryIdC}";
	product2["category_name_c"] = "${categoryNameC}";
	product2["quantity"] = ${quantity}; // intiger
	product2["revenue"] = ${revenue}; // intiger
	// 구매된 상품의 코드, 명칭, 브랜드명, 카테고리 대-중-소, 수량, 매출액으로 치환
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	purchase["product"] = productArray;
	DOT.logPurchase(purchase);
</script>
```



### 적용예시

*필터를 바꿔쓰는 수압 센 샤워헤드_실버* 상품 1개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object();
	purchase["transaction_id"] = "TR2020080418284";
	purchase["currency"] = "KRW";
	var product1 = new Object();
	product1["product_id"] = "01P0000237409";
	product1["product_name"] = "필터를 바꿔쓰는 수압 센 샤워헤드_실버";
	product1["brand_name"] = "J1";
	product1["category_id_a"] = "010000000010";
	product1["category_name_a"] = "욕실";
	product1["category_id_b"] = "010000000104";
	product1["category_name_b"] = "욕실소품";
	product1["quantity"] = 1;
	product1["revenue"] = 19900;
	purchase["product"] = product1;
	DOT.logPurchase(purchase);
</script>
```



*필터를 바꿔쓰는 수압 센 샤워헤드_실버* 상품 1개와 *아쿠아 디 콜로니아 - 프리지아* 상품 2개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object();
	purchase["transaction_id"] = "TR202008052278";
	purchase["currency"] = "KRW";
	var product1 = new Object();
	product1["product_id"] = "01P0000237409";
	product1["product_name"] = "필터를 바꿔쓰는 수압 센 샤워헤드_실버";
	product1["brand_name"] = "J1";
	product1["category_id_a"] = "010000000010";
	product1["category_name_a"] = "욕실";
	product1["category_id_b"] = "010000000104";
	product1["category_name_b"] = "욕실소품";
	product1["quantity"] = 1;
	product1["revenue"] = 19900;
	var product2 = new Object();
	product2["product_id"] = "01P0000256908";
	product2["product_name"] = "안전 면봉_80P";
	product2["brand_name"] = "J1";
	product2["category_id_a"] = "2004016066";
	product2["category_name_a"] = "헬스/뷰티";
	product2["category_id_b"] = "2004016073";
	product2["category_name_b"] = "미용소품";
	product2["quantity"] = 2;
	product2["revenue"] = 2000;
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	purchase["product"] = productArray;
	DOT.logPurchase(purchase);
</script>
```



## 개별 화면 조회 측정

아래 매핑 테이블에 정리한 화면들의 조회수를 측정하기 위해 **해당 화면 내에 API**를 추가합니다. 매핑 테이블에서 eventId 와 pageId 를 참고하여 API를 적용해주세요.



### 매핑 테이블


| 번호 | 화면        | eventId   | pageId    | 설명                  |
| :--: | ----------- | --------- | --------- | --------------------- |
|  1  | 메인        | w_view_home | home | /initMain.siv         |
|  2   | 인기/추천 | view_best | best | /initMain.siv#hCtge1#hPage1   |
|  3   | 신상품/인기상품 | view_best | best_new | /searchBestAndNew.siv |



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "${eventId}";
	screen["page_id"] = "${pageId}";
	// 매핑 테이블을 참고하여 eventId 와 pageId 를 치환하여 적용
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 메인 화면을 조회한 경우 해당 화면 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_home";
	screen["page_id"] = "home";
	DOT.logScreen(screen);
</script>
```



유저가 신상품/인기상품 화면을 조회한 경우 해당 화면 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "view_best";
	screen["page_id"] = "best_new";
	DOT.logScreen(screen);
</script>
```



## 장바구니 조회 측정

장바구니(쇼핑백) 화면의 조회수를 측정하기 위해 **쇼핑백 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_cart";
	screen["page_id"] = "cart";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandCode}";
	// 쇼핑백 화면에 존재하는 상품의 코드, 명칭, 브랜드코드로 치환
	product1["quantity"] = ${quantity}; // intiger
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandCode}";
	// 쇼핑백 화면에 존재하는 상품의 코드, 명칭, 브랜드코드로 치환
	product2["quantity"] = ${quantity}; // intiger
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
```



### 적용예시

*회전하는 리버스윈드 무선 서큘레이터* 상품 1개가 쇼핑백 화면 내에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_cart";
	screen["page_id"] = "cart";
	var product1 = new Object();
	product1["product_id"] = "2003258930";
	product1["product_name"] = "회전하는 리버스윈드 무선 서큘레이터";
	product1["brand_name"] = "J1";
	product1["quantity"] = 1;
	screen["product"] = product1;
	DOT.logScreen(screen);
</script>
```



*회전하는 리버스윈드 무선 서큘레이터* 상품 1개와 *UNI 시어서커 5부 파자마 상하 세트* 상품 2개가 쇼핑백 화면 내에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_cart";
	screen["page_id"] = "cart";
	var product1 = new Object();
	product1["product_id"] = "2003258930";
	product1["product_name"] = "회전하는 리버스윈드 무선 서큘레이터";
	product1["brand_name"] = "J1";
	product1["quantity"] = 1;
	var product2 = new Object();
	product2["product_id"] = "2003256249";
	product2["product_name"] = "UNI 시어서커 5부 파자마 상하 세트";
	product2["brand_name"] = "J1";
	product2["quantity"] = 2;
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
```



## 카테고리 화면 조회 측정

'카테고리 화면'이란 GNB에서 '홈'과 '인기/추천'을 제외한 나머지 메뉴들을 클릭하면 연결되는 화면들을 말합니다. 각 **카테고리 화면 내**에 API를 적용해야 하며 아래 정리한 내용을 참고하여 적용해 주세요.

* 각 카테고리를 구분하기 위해 화면마다 pageId 값이 달라지게 됩니다. 예를 들어 '에슬레저' 화면과 '헬스/뷰티' 화면의 pageId 값은 달라야 합니다. 이렇게 변경되는 코드값은 매핑 테이블을 참고해서 적용해 주시기 바랍니다.
* 대 카테고리 화면에서는 대 카테고리 정보만 수집하고, 중 카테고리 화면에서는 대 + 중 카테고리 정보를 모두 수집하는 형태입니다.



### 매핑 테이블

| 번호 | 카테고리 | pageId | pageId |
| :--: | --- | --- | --- |
|  1   | 에슬레져      | athleisure | 에슬레져 하위 카테고리 화면에도 동일한 pageId 적용      |
|  2   | 헬스/뷰티      | hnb   | 헬스/뷰티 하위 카테고리 화면에도 동일한 pageId 적용      |
|  3   | 언더웨어       | underwear | 언더웨어 하위 카테고리 화면에도 동일한 pageId 적용          |
|  4   | 슬립웨어       | sleepwear | 슬립웨어 하위 카테고리 화면에도 동일한 pageId 적용          |
|  5   | 패션         | fashion | 패션 하위 카테고리 화면에도 동일한 pageId 적용          |
|  6   | 홈데코        | homedeco | 홈데코 하위 카테고리 화면에도 동일한 pageId 적용          |
|  7   | 가전 | appliance | 가전 하위 카테고리 화면에도 동일한 pageId 적용 |
|  8   | 침구 | bedding | 침구 하위 카테고리 화면에도 동일한 pageId 적용 |
|  9   | 주방 | kitchen | 주방 하위 카테고리 화면에도 동일한 pageId 적용 |
|  10   | 욕실 | bath | 욕실 하위 카테고리 화면에도 동일한 pageId 적용 |
|  11   | 가구수납 | furniture | 가구수납 하위 카테고리 화면에도 동일한 pageId 적용 |
|  12   | 트래블 | travel | 트래블 하위 카테고리 화면에도 동일한 pageId 적용 |



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_category";
	screen["page_id"] = "${pageId}";
	// 매핑 테이블을 참고해 pageId 값을 치환하여 적용
	screen["category_id_a"] = "${categoryIdA}";
	screen["category_name_a"] = "${categoryNameA}";
	screen["category_id_b"] = "${categoryIdB}";
	screen["category_name_b"] = "${categoryNameB}";
	screen["category_id_c"] = "${categoryIdC}";
	screen["category_name_c"] = "${categoryNameC}";
	// 해당 화면의 카테고리 대-중-소 정보를 치환하여 적용
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *헬스/뷰티* 카테고리를 조회한 경우 해당 화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_category";
	screen["page_id"] = "hnb";
	screen["category_id_a"] = "2004016066";
	screen["category_name_a"] = "헬스/뷰티";
	DOT.logScreen(screen);
</script>
```



유저가 *에슬레져 > 상의* 카테고리를 조회한 경우 해당 화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_category";
	screen["page_id"] = "athleisure";
	screen["category_id_a"] = "2004015921";
	screen["category_name_a"] = "애슬레저";
	screen["category_id_b"] = "2004016062";
	screen["category_name_b"] = "상의";
	DOT.logScreen(screen);
</script>
```



## 기획전 조회 측정

개별 기획전의 조회수를 측정하기 위해 **기획전 상세 화면 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_exhibition";
	screen["page_id"] = "exhibition";
	screen["exhibition_id"] = "${exhibitionId}";
	screen["exhibition_name"] = "${exhibitionName}";
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *올 여름 마지막 캠핑* 기획전을 조회한 경우 해당 기획전 상세화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_exhibition";
	screen["page_id"] = "exhibition";
	screen["exhibition_id"] = "2007020168";
	screen["exhibition_name"] = "올 여름 마지막 캠핑";
	DOT.logScreen(screen);
</script>
```



## 기획전 공유하기 측정

기획전 상세 화면에 있는 공유하기 버튼의 클릭수를 측정하기 위해 **해당 버튼이 클릭된 시점**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "w_share";
	event["share_type"] = "exhibition";
	event["exhibition_id"] = "${exhibitionId}";
	event["exhibition_name"] = "${exhibitionName}";
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *올 여름 마지막 캠핑* 기획전의 공유 버튼을 클릭한 경우 버튼이 클릭된 시점에 아래와 같이 적용

``` javascript
function exhibitionShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "exhibition";
	event["exhibition_id"] = "2007020168";
	event["exhibition_name"] = "올 여름 마지막 캠핑";
	DOT.logEvent(event);
}

onclick="exhibitionShare()"
```



## App Push 동의 여부 측정

유저가 App Push에 대해 동의 또는 비동의 하는 횟수를 측정하기 위해 API를 적용합니다. 유저가 **동의 또는 비동의한 시점**에 API를 적용해주세요. 앱 푸시 동의/비동의가 변경되는 모든 펑션에 본 API가 적용되어야 합니다.



### 측정 API

``` javascript
DOT.setUser(User.setAttr5("${attr5Code}"));
/*
	유저가 동의한 경우 opt-in
	유저가 비동의한 경우 opt-out
	
	동의 여부에 따라 attr5Code를 위 값으로 치환하여 적용
*/

var event = new Object();
event["event"] = "${eventCode}";
/*
	유저가 동의한 경우 w_notification_opt_in
	유저가 비동의한 경우 w_notification_opt_out
	
	동의 여부에 따라 eventCode를 위 값으로 치환하여 적용
*/
DOT.logEvent(event);
```



### 적용예시

유저가 '광고성 알림 받기'에 체크표시를 하여 App Push 수신에 동의한 경우 아래와 같이 적용

``` javascript
function appPushChk() {
	alert("알림 수신이 설정되었습니다. (전송자: 신세계인터내셔날)");
    
	DOT.setUser(User.setAttr5("opt-in"));
	var event = new Object();
	event["event"] = "w_notification_opt_in";
	DOT.logEvent(event);
}
```



## 적용 후 데이터 검증

SDK와 API가 올바르게 적용 되었는지 확인하기 위해서는 아래 코드(디버그 모드 활성화)를 적용한 테스트 앱을 저희 쪽으로 보내주시면 됩니다. 보내주신 테스트 앱에서 데이터를 확인한 후 결과에 대해서 회신 드리고 있습니다.

### AOS

AndroidManifest.xml 파일에 아래 메타 데이터 태그를 추가합니다.

``` kotlin
<meta-data android:name="WiseTrackerLogState" android:value="true" />
// 개발용 테스트 앱에는 true로, 배포용 앱에는 false로 설정
```



### iOS

Info.plist 파일에 아래 그림과 같이 값을 추가 합니다.

![iOS Debug Mode](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
