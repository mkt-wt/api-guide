# Wisetracker Integration Guide

와이즈트래커 2.0을 'S.I.Village' 앱에 연동하기 위한 내용을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.



> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [SDK 적용](./siv_20.md#SDK-적용)
* [회원가입 측정](./siv_20.md#회원가입-측정)
* [JAJU클럽 가입 측정](./siv_20.md#JAJU클럽-가입-측정)
* [뷰티클럽 가입 측정](./siv_20.md#뷰티클럽-가입-측정)
* [마이 브랜드에 추가 측정](./siv_20.md#마이-브랜드에-추가-측정)
* [로그인 측정](./siv_20.md#로그인-측정)
* [검색 측정](./siv_20.md#검색-측정)
* [상품 조회 측정](./siv_20.md#상품-조회-측정) -> (w_view_product 이벤트를 명시적으로 세팅해줘야 하는것 아닌지 확인 필요)
* [상품 리뷰 조회 측정](./siv_20.md#상품-리뷰-조회-측정) -> (1개의 상품에 대해 조회가 이루어지므로 product  오브젝트를 1개 생성)
* [상품 공유하기 측정](./siv_20.md#상품-공유하기-측정) -> (1개의 상품에 대해 궁유가 이루어지므로 product  오브젝트를 1개 생성)
* [공유하기 측정](./siv_20.md#공유하기-측정)
* [위시리스트에 담기 측정](./siv_20.md#위시리스트에-담기-측정) -> (1개 상품, 2개 이상의 상품에 대한 가이드 확인 필요)
* [장바구니 담기 측정](./siv_20.md#장바구니-담기-측정) -> (1개 상품, 2개 이상의 상품에 대한 가이드 확인 필요)
* [주문 시작 측정](./siv_20.md#주문-시작-측정) -> (상품 오브젝트 내에 카테고리, 브랜드 디멘전이 포함되어 있는데 문제 없는지)
* [구매 완료 측정](./siv_20.md#구매-완료-측정) -> (상품 오브젝트 내에 카테고리, 브랜드 디멘전이 포함되어 있는데 문제 없는지)
* [개별 메인 화면 조회 측정](./siv_20.md#개별-메인-화면-조회-측정)
* [카테고리 화면 조회 측정](./siv_20.md#카테고리-화면-조회-측정)
* [기획전 조회 측정](./siv_20.md#기획전-조회-측정)
* [이벤트 조회 측정](./siv_20.md#기획전-조회-측정)
* [매거진 조회 측정](./siv_20.md#기획전-조회-측정)
* [브랜드관 조회 측정](./siv_20.md#브랜드관-조회-측정)
* [위시리스트 조회 측정](./siv_20.md#위시리스트-조회-측정) -> (2개 이상의 상품이 화면 내에 있을때에 대한 처리)
* [장바구니 조회 측정](./siv_20.md#장바구니-조회-측정) -> (2개 이상의 상품이 화면 내에 있을때에 대한 처리)
* [메뉴 클릭 측정](./siv_20.md#메뉴-클릭-측정)
* [배너 클릭 측정](./siv_20.md#배너-클릭-측정)
* [아이템 클릭 측정](./siv_20.md#아이템-클릭-측정)
* [팝업 클릭 측정](./siv_20.md#팝업-클릭-측정)
* [재입고 알림신청 측정](./siv_20.md#재입고-알림신청-측정)
* [App Push 동의 여부 측정](./siv_20.md#App-Push-동의-여부-측정)
* [쿠폰 다운로드 측정](./siv_20.md#쿠폰-다운로드-측정)
* [적용 후 데이터 검증](./siv_20.md#적용-후-데이터-검증)
  * [AOS](./siv_20.md#AOS)
  * [iOS](./siv_20.md#iOS)



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
	event["signupTp"] = "${signupTp}";
	/*
		signupTp 는
		본인인증가입 또는 간편가입
		둘 중 하나로 치환하여 적용
	*/
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 본인인증 가입을 통해 회원가입을 완료한 경우 완료 화면에 아래와 같이 적용

```html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_signup_complete";
	event["signupTp"] = "본인인증가입";
	DOT.logEvent(event);
</script>
```



## JAJU클럽 가입 측정

유저가 JAJU클럽으로 가입한 횟수를 측정하기 위해 **클럽 가입이 완료된 시점**에 API를 적용합니다. 아래 두 가지 경우에 모두 적용되어야 합니다.

1. 회원가입 프로세스에서 '자주클럽'에 체크 표시를 한 경우
2. 마이페이지 > 관심클럽에서 자주클럽에 가입한 경우



### 측정 API & 적용예시

``` javascript
function joinJajuClub() {
	...
	alert("자주클럽에 가입 되었습니다.");
	var event = new Object();
	event["event"] = "join_jajuclub";
    event["g102"] = 1;
	DOT.logEvent(event);
}
```



## 뷰티클럽 가입 측정

유저가 뷰티클럽으로 가입한 횟수를 측정하기 위해 **클럽 가입이 완료된 시점**에 API를 적용합니다. 아래 두 가지 경우에 모두 적용되어야 합니다.

1. 회원가입 프로세스에서 '뷰티클럽'에 체크 표시를 한 경우
2. 마이페이지 > 관심클럽에서 뷰티클럽에 가입한 경우



### 측정 API & 적용예시

``` javascript
function joinBtyClub() {
	...
	alert("뷰티클럽에 가입 되었습니다.");
	var event = new Object();
	event["event"] = "join_beautyclub";
    event["g102"] = 1;
	DOT.logEvent(event);
}
```



## 마이 브랜드에 추가 측정

각 브랜드가 마이 브랜드로 추가되는 것을 측정하기 위해 API를 적용합니다. 앱 내의 아래 메뉴에서 마이 브랜드로 추가하는 이벤트가 발생합니다.

* 회원가입 과정에서 관심 있는 My Brand 정보 체크 시
* 햄버거 메뉴를 통해 브랜드 탭으로 이동하여 각 브랜드 옆에 별표 클릭 시



위의 경로를 통해 특정 브랜드가 성공적으로 마이 브랜드에 추가된 시점에 API를 적용해 주시기 바랍니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "add_to_mybrand";
	event["g100"] = 1;
	event["brand_name"] = "${brandName}";
	// brandName 은 마이 브랜드로 추가된 브랜드의 명칭으로 치환
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 햄버거 메뉴에서 Byredo 를 마이 브랜드로 추가한 경우 아래와 같이 적용

``` javascript
var event = new Object();
event["event"] = "add_to_mybrand";
event["g100"] = 1;
event["brand_name"] = "Byredo";
DOT.logEvent(event);
// 특정 브랜드가 마이 브랜드로 등록된 조건문에 위 코드 추가 
```



## 로그인 측정

로그인 횟수와 유저 정보를 측정하기 위해 **로그인 완료 시점**에 API를 적용합니다. 아래에 리스팅된 정보는 반드시 매핑 테이블을 참고하여 적용해 주시기 바랍니다.

1. 회원 성별
2. 회원 연령대
3. 회원 유형 - 일반 회원 / 임직원 구분
4. 회원 등급 - SI 멤버십 등급에 따른 구분
5. App Push 동의 여부
6. 로그인 유형 - ID 또는 소셜 로그인 구분



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



#### App Push 동의 여부

| 동의 여부 | attr3Code |
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
	.setAttr3("${attr3Code}"));
	// 매핑 테이블을 참고하여 치환

var event = new Object();
event["event"] = "w_login_complete";
event["loginTp"] = "${loginTp}"; // 매핑 테이블을 참고하여 치환
DOT.logEvent(event);
```



### 적용예시

Gold 등급의 31세 여성이며 임직원이 아니며 App Push 수신에 동의한 회원이 카카오 계정으로 로그인한 경우, 로그인 완료 시점에 아래와 같이 적용

```javascript
DOT.setUser(User.setGender("female")
	.setAge("30-34")
	.setAttr1("member")
	.setAttr2("gold")
	.setAttr3("opt-in"));

var event = new Object();
event["event"] = "w_login_complete";
event["loginTp"] = "kakao";
DOT.logEvent(event);
```



## 검색 측정

유저의 *검색 방법* 과 *검색어*를 측정하기 위해 API를 적용합니다. 반드시 아래 사항을 참고하여 적용해 주시기 바랍니다.

* 본 API는 **검색 완료 화면 내**에서 호출하는 것이 기본값입니다.
* 그러나 유저의 *검색 방법* 을 측정하기 위해, 경우에 따라 **검색어 클릭 시점**에 API를 호출해도 문제 없습니다.

* 예를 들어 *일반적인 검색* (form에 검색어를 넣고 엔터 또는 돋보기 버튼 클릭)이라면 검색 완료 화면에서 API를 호출합니다.
* 그러나 *검색 방법* (추천/최근/자동완성 검색)을 구분해서 측정해야 하기 때문에, 검색 완료 화면에서 이 정보를 유지할 수 없는 경우라면 **해당 검색어가 클릭된 시점**에 API를 호출하면 됩니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_search";
	event["search_type"] = "${searchType}";
	/*
		일반적인 검색은 normal
		추천검색어는 rcm_keyword
		최근검색어는 recent_keyword
		자동검색어는 auto_keyword
		
		위 설명에 따라 searchType 을 치환
	*/
	event["search_term"] = "${searchTerm}";
	// 검색된 키워드로 치환
	event["g20"] = ${numberOfResults}; // integer
	// 검색 결과로 출력된 '상품 item'의 개수 (기획전, 매거진 제외)
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 "제이린드버그"를 입력하고 돋보기 버튼을 클릭한 경우, **검색 완료 화면**에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_search";
	event["search_type"] = "normal";
	event["search_term"] = "제이린드버그";
	event["g20"] = 1981;
	DOT.logEvent(event);
</script>
```



유저가 자동검색어 영역에 출력된 "디젤 로고 미니 백팩" 키워드를 클릭하여 검색이 진행된 경우, ***검색 방법* 을 수집할 수 있는 시점**에 API 적용

``` javascript
function fnReSearch(keyword, searchType) {
	var event = new Object();
	event["event"] = "w_search";
	event["search_type"] = "auto_keyword";
	event["search_term"] = "디젤 로고 미니 백팩";
	/*
		만약 검색어 클릭 시 ${numberOfResults} 를 수집할 수 없다면
		event["g20"] = ${numberOfResults}; 라인은 적용하지 않음
	*/
	DOT.logEvent(event);
}
```



## 상품 조회 측정

개별 상품의 조회수를 측정하기 위해 **상품 상세 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_product";
	screen["page_id"] = "goods";
	
	var product = new Object();
	product["product_id"] = "${productId}";
	product["product_name"] = "${productName}";
	product["brand_name"] = "${brandName}";
	product["category_id_a"] = "${categoryIdA}";
	product["category_name_a"] = "${categoryNameA}";
	product["category_id_b"] = "${categoryIdB}";
	product["category_name_b"] = "${categoryNameB}";
	product["category_id_c"] = "${categoryIdC}";
	product["category_name_c"] = "${categoryNameC}";
	// 조회된 상품의 코드, 명칭, 브랜드, 카테고리 대-중-소 정보로 치환
	
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



### 적용예시

*퍼프 슬리브 셔링 원피스* 상품이 조회된 경우 해당 페이지 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_product";
	screen["page_id"] = "goods";
	var product = new Object();
	product["product_id"] = "2005272698";
	product["product_name"] = "퍼프 슬리브 셔링 원피스";
	product["brand_name"] = "VOV";
	product["category_id_a"] = "1";
	product["category_name_a"] = "여성패션";
	product["category_id_b"] = "010000029453";
	product["category_name_b"] = "원피스/점프수트";
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



## 상품 리뷰 조회 측정

각 상품별로 리뷰 조회수를 측정하기 위해 API를 적용합니다. 아래 두 조건 중 더 적용하기 편리한 위치에 API를 적용해 주시기 바랍니다.

* 상품 상세화면에 있는 상품 리뷰 *버튼 클릭 시점*
* 또는 *상품 리뷰 레이어 내*



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_see_review";
	var product = new Object();
	product["product_id"] = "${productId}";
	product["product_name"] = "${productName}";
	product["brand_name"] = "${brandName}";
	// 리뷰가 조회된 상품의 코드, 명칭, 브랜드명으로 치환
	product["category_id_a"] = "${categoryIdA}";
	product["category_name_a"] = "${categoryNameA}";
	// 리뷰가 조회된 상품의 대 카테고리 코드와 명칭으로 치환
	product["category_id_b"] = "${categoryIdB}";
	product["category_name_b"] = "${categoryNameB}";
	// 리뷰가 조회된 상품의 중 카테고리 코드와 명칭으로 치환
	product["category_id_C"] = "${categoryIdC}";
	product["category_name_C"] = "${categoryNameC}";
	// 리뷰가 조회된 상품의 소 카테고리 코드와 명칭으로 치환
	event["product"] = product;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *레오파드 셔츠 블라우스* 상품 상세화면에서 리뷰 버튼을 클릭한 경우 아래와 같이 적용

``` javascript
var event = new Object();
event["event"] = "w_see_review";
var product = new Object();
product["product_id"] = "2002247930";
product["product_name"] = "레오파드 셔츠 블라우스";
product["brand_name"] = "STUDIO TOMBOY";
product["category_id_a"] = "0";
product["category_name_a"] = "여성패션";
product["category_id_b"] = "010000029439";
product["category_name_b"] = "셔츠/블라우스";
event["product"] = product;
DOT.logEvent(event);
```



## 공유하기 측정

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
	product["brand_name"] = "${brandName}";
	// 상품코드 상품명 브랜드명으로 치환
	event["product"] = product;
	DOT.logEvent(event);
</script>
```



### 적용예시

*브로 레인지파인더 케이스* 상품의 **공유버튼이 클릭**된 시점에 아래와 같이 적용

``` javascript
function productShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "product";
    var product = new Object();
	product["product_id"] = "2003258434";
	product["product_name"] = "브로 레인지파인더 케이스";
	product["brand_name"] = "J.LINDEBERG";
    event["product"] = product;
	DOT.logEvent(event);
}

onclick="productShare()"
```



## 공유하기 측정

상품 공유 외에도 아래 세 가지 유형의 '공유하기'가 존재합니다. 해당 화면의 **공유하기 버튼이 클릭되는 시점**에 API를 적용해 주세요.

1. 이벤트 공유하기
2. 기획전 공유하기
3. 매거진 공유하기



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "w_share";
	event["share_type"] = "${shareType}";
	/* 
		이벤트를 공유한 경우 event
		기획전을 공유한 경우 shop
		매거진을 공유한 경우 magazine
		
		위 설명에 따라 shareType 을 치환
	*/
	event["event_id"] = "${eventId}";
	event["event_name"] = "${eventName}";
	// 위 2 라인은 이벤트 공유시에만 사용, 이벤트코드와 이벤트명으로 치환
	event["shop_id"] = "${shopId}";
	event["shop_name"] = "${shopName}";
	// 위 2 라인은 기획전 공유시에만 사용, 기획전코드와 기획전명으로 치환
	event["content_id"] = "${contentId}";
	event["content_name"] = "${contentName}";
	// 위 2 라인은 매거진 공유시에만 사용, 매거진코드와 매거인명으로 치환
	DOT.logEvent(event);
</script>
```



### 적용예시

**이벤트 공유하기**

*딥티크 나만의 여행용 향수 FLEX* 이벤트의 **공유버튼이 클릭**된 시점에 아래와 같이 적용

``` javascript
function eventShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "event";
	event["event_id"] = "E200705025";
	event["event_name"] = "딥티크 나만의 여행용 향수 FLEX";
	DOT.logEvent(event);
}

onclick="eventShare()"
```



**기획전 공유하기**

*아크테릭스, SIV 런칭!* 기획전의 **공유버튼이 클릭**된 시점에 아래와 같이 적용

``` javascript
function shopShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "shop";
	event["shop_id"] = "2007019421";
	event["shop_name"] = "아크테릭스, SIV 런칭!";
	DOT.logEvent(event);
}

onclick="shopShare()"
```



**매거진 공유하기**

*원피스를 트렌디하게 입는 방법* 매거진의 **공유버튼이 클릭**된 시점에 아래와 같이 적용

``` javascript
function magazineShare() {
	var event = new Object();
	event["event"] = "w_share";
	event["share_type"] = "magazine";
	event["content_id"] = "2007019748";
	event["content_name"] = "원피스를 트렌디하게 입는 방법";
	DOT.logEvent(event);
}

onclick="magazineShare()"
```



## 위시리스트에 담기 측정

상품이 위시리스트에 추가된 횟수를 측정하기 위해 API를 적용합니다. 아래와 같은 경우에 모두 적용되어야 합니다.

* 리스트 화면(검색 결과, 기획전 상세, 이벤트 상세, 개별 카테고리 화면)에 배치된 상품 이미지의 '별표' 클릭
* 상품 상세 하단 Bar에 있는 '별표' 클릭
* 쇼핑백 화면 내의 위시리스트 버튼 클릭



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_add_to_wishlist";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandName}";
	// 위시리스트에 추가된 상품의 코드, 명칭, 브랜드명으로 치환
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	// 위시리스트에 추가된 상품의 코드, 명칭, 브랜드명으로 치환
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	event["product"] = productArray;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *호일 로고 배너 반팔 티셔츠* 상품을 위시리스트에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
    var event = new Object();
    event["event"] = "w_add_to_wishlist";
    var product1 = new Object();
	product1["product_id"] = "1903174091";
	product1["product_name"] = "호일 로고 배너 반팔 티셔츠";
	product1["brand_name"] = "ED HARDY";
    event["product"] = product1;
	DOT.logEvent(event);
}
```



유저가 *호일 로고 배너 반팔 티셔츠* 상품과 *브로 볼 케이스* 상품을 위시리스트에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_wishlist";
    var product1 = new Object();
	product1["product_id"] = "1903174091";
	product1["product_name"] = "호일 로고 배너 반팔 티셔츠";
	product1["brand_name"] = "ED HARDY";
    var product2 = new Object();
	product2["product_id"] = "2003258435";
	product2["product_name"] = "브로 볼 케이스";
	product2["brand_name"] = "J.LINDEBERG";
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
	product1["brand_name"] = "${brandName}";
	// 장바구니에 추가된 상품의 코드, 명칭, 브랜드명으로 치환
	product1["quantity"] = ${quantity}; // intiger
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	// 장바구니에 추가된 상품의 코드, 명칭, 브랜드명으로 치환
	product2["quantity"] = ${quantity}; // intiger
	
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	event["product"] = productArray;
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 *호일 로고 배너 반팔 티셔츠* 상품 2개를 장바구니에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_cart";
    var product1 = new Object();
	product1["product_id"] = "1903174091";
	product1["product_name"] = "호일 로고 배너 반팔 티셔츠";
	product1["brand_name"] = "ED HARDY";
    product1["qunatity"] = 2;
    event["product"] = product1;
	DOT.logEvent(event);
}
```



유저가 *호일 로고 배너 반팔 티셔츠* 상품 2개와 *브로 볼 케이스* 상품 1개를 장바구니에 추가한 경우, 추가 완료 시점에 아래와 같이 적용

``` javascript
function addToCart() {
	var event = new Object();
	event["event"] = "w_add_to_cart";
    var product1 = new Object();
	product1["product_id"] = "1903174091";
	product1["product_name"] = "호일 로고 배너 반팔 티셔츠";
	product1["brand_name"] = "ED HARDY";
    product1["qunatity"] = 2;
    var product2 = new Object();
	product2["product_id"] = "2003258435";
	product2["product_name"] = "브로 볼 케이스";
	product2["brand_name"] = "J.LINDEBERG";
    product2["qunatity"] = 1;
    var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
    event["product"] = productArray;
	DOT.logEvent(event);
}
```



## 주문 시작 측정

상품에 대한 주문 절차를 시작하는 행동을 측정하기 위해 **주문서 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_init_checkout";
	screen["page_id"] = "initorder";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandName}";
	product1["quantity"] = ${quantity}; // intiger
	// 주문서에 존재하는 상품의 코드, 명칭, 브랜드명, 수량으로 치환
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	product2["quantity"] = ${quantity}; //intiger
	// 주문서에 존재하는 상품의 코드, 명칭, 브랜드명, 수량으로 치환
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	screen["product"] = productArray;
	
	DOT.logScreen(screen);
</script>
```




### 적용예시

*5AC 패밀리 백* 상품 1개가 주문서에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_init_checkout";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["quantity"] = 1;
	screen["product"] = product1;
	DOT.logScreen(screen);
</script>
```



*5AC 패밀리 백* 상품 1개와 *아쿠아 디 콜로니아 - 프리지아* 상품 2개가 주문서에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_init_checkout";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["quantity"] = 1;
	var product2 = new Object();
	product2["product_id"] = "01P0000116871";
	product2["product_name"] = "아쿠아 디 콜로니아 - 프리지아";
	product2["brand_name"] = "SANTA MARIA NOBELLA";
	product2["quantity"] = 2;
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
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

*5AC 패밀리 백* 상품 1개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object();
	purchase["transaction_id"] = "TR2020080418284";
	purchase["currency"] = "KRW";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["category_id_a"] = "3";
	product1["category_name_a"] = "잡화";
	product1["category_id_b"] = "010000029638";
	product1["category_name_b"] = "남성가방";
	product1["quantity"] = 1;
	product1["revenue"] = 1490000;
	purchase["product"] = product1;
	DOT.logPurchase(purchase);
</script>
```



*5AC 패밀리 백* 상품 1개와 *아쿠아 디 콜로니아 - 프리지아* 상품 2개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object();
	purchase["transaction_id"] = "TR202008052278";
	purchase["currency"] = "KRW";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["category_id_a"] = "3";
	product1["category_name_a"] = "잡화";
	product1["category_id_b"] = "010000029638";
	product1["category_name_b"] = "남성가방";
	product1["quantity"] = 1;
	product1["revenue"] = 1490000;
	var product2 = new Object();
	product2["product_id"] = "01P0000116871";
	product2["product_name"] = "아쿠아 디 콜로니아 - 프리지아";
	product2["brand_name"] = "SANTA MARIA NOBELLA";
	product2["category_id_a"] = "6";
	product2["category_name_a"] = "뷰티";
	product2["category_id_b"] = "010000002007";
	product2["category_name_b"] = "향수";
	product2["quantity"] = 2;
	product2["revenue"] = 284800;
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	purchase["product"] = productArray;
	DOT.logPurchase(purchase);
</script>
```



## 개별 메인 화면 조회 측정

아래 매핑 테이블에 정리한 화면들의 조회수를 측정하기 위해 **해당 화면 내에 API**를 추가합니다. 매핑 테이블에서 eventId 와 pageId 를 참고하여 API를 적용해주세요.



### 매핑 테이블


| 번호 | 메인 화면          | eventId              | pageId    | 설명                         |
| :--: | ------------------ | -------------------- | --------- | ---------------------------- |
|  1   | 셀렉트449 메인     | view_select_main     | select449 | /initDGMain.siv              |
|  2   | 이벤트 메인        | view_event_main      | eventmain | /initEventMain.siv           |
|  3   | 기획전 메인        | view_shop_main       | shopmain  | /initPlanShopMain.siv        |
|  4   | 아울렛 메인        | view_outlet_main     | outlet    | /initOutlet.siv              |
|  5   | 매거진 메인        | view_mgz_main        | mzg       | /initMagazineMain.siv        |
|  6   | 마이페이지 메인    | view_mypage_main     | mypage    | /initMypageMain.siv          |
|  7   | 마이쿠폰           | view_mycoupon        | mycoupon  | /searchCpn.siv               |
|  8   | 회원가입 유형 선택 | signup_jointype      | 0jointype | /joinType.siv                |
|  9   | 회원가입 본인인증  | signup_authorization | 0auth     | /authorization.siv           |
|  10  | 회원가입 정보입력  | signup_join          | 0join     | 인증 이후 회원 정보 입력화면 |



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

유저가 매거진 메인화면을 조회한 경우 해당 화면 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "view_mgz_main";
	screen["page_id"] = "mzg";
	DOT.logScreen(screen);
</script>
```



유저가 매거진 회원가입 본인인증 화면을 조회한 경우 해당 화면 내에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "signup_authorization";
	screen["page_id"] = "0auth";
	DOT.logScreen(screen);
</script>
```



## 카테고리 화면 조회 측정

'카테고리 화면'이란 햄버거메뉴의 카테고리 탭을 통해 진입할 수 있는 화면들(/initDispCtg.siv)을 의미합니다. 각 카테고리별 조회수를 측정하기 위해 **카테고리 화면 내**에 API를 적용합니다.  반드시 아래 매핑 테이블을 참고해주세요



### 매핑 테이블

| 번호 | 카테고리 화면 | pageId   | 설명                                                      |
| :--: | ------------- | -------- | --------------------------------------------------------- |
|  1   | 여성패션      | women    | 여성패션의 하위 카테고리 화면에도 동일한 pageId 적용      |
|  2   | 남성패션      | men      | 남성패션의 하위 카테고리 화면에도 동일한 pageId 적용      |
|  3   | 잡화          | acc      | 잡화의 하위 카테고리 화면에도 동일한 pageId 적용          |
|  4   | 아동          | kids     | 아동의 하위 카테고리 화면에도 동일한 pageId 적용          |
|  5   | 뷰티          | beauty   | 뷰티의 하위 카테고리 화면에도 동일한 pageId 적용          |
|  6   | 생활          | living   | 생활의 하위 카테고리 화면에도 동일한 pageId 적용          |
|  7   | 가구/인테리어 | interior | 가구/인테리어의 하위 카테고리 화면에도 동일한 pageId 적용 |



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

유저가 *여성패션 > 코트 > 더플 코트* 카테고리를 조회한 경우 해당 화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_category";
	screen["page_id"] = "women";
	screen["category_id_a"] = "010000029407";
	screen["category_name_a"] = "여성패션";
	screen["category_id_b"] = "010000029408";
	screen["category_name_b"] = "코트";
	screen["category_id_c"] = "010000029410";
	screen["category_name_c"] = "더플 코트";
	DOT.logScreen(screen);
</script>
```



## 기획전 조회 측정

개별 기획전의 조회수를 측정하기 위해 **기획전 상세 화면 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_shop";
	screen["page_id"] = "shop";
	screen["shop_id"] = "${shopId}";
	screen["shop_name"] = "${shopName}";
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *[alexanderwang] OUTLET FURTHER MARKDOWN* 기획전을 조회한 경우 해당 기획전 상세화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_shop";
	screen["page_id"] = "shop";
	screen["shop_id"] = "2007019342";
	screen["shop_name"] = "[alexanderwang] OUTLET FURTHER MARKDOWN";
	DOT.logScreen(screen);
</script>
```



## 이벤트 조회 측정

개별 이벤트의 조회수를 측정하기 위해 **이벤트 상세 화면 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_event";
	screen["page_id"] = "event";
	screen["event_id"] = "${eventId}";
	screen["event_name"] = "${eventName}";
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *삼성카드 보너스클럽 제휴 OPEN* 이벤트를 조회한 경우 해당 이벤트 상세화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_event";
	screen["page_id"] = "event";
	screen["event_id"] = "2007019342";
	screen["event_name"] = "삼성카드 보너스클럽 제휴 OPEN";
	DOT.logScreen(screen);
</script>
```



## 매거진 조회 측정

개별 매거진의 조회수를 측정하기 위해 **매거진 상세 화면 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_content";
	screen["page_id"] = "magazine";
	screen["content_id"] = "${scratId}";
	screen["content_name"] = "${scratName}";
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *발끝의 자부심, 팔케* 매거진을 조회한 경우 해당 매거진 상세화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_content";
	screen["page_id"] = "magazine";
	screen["content_id"] = "2007019754";
	screen["content_name"] = "발끝의 자부심, 팔케";
	DOT.logScreen(screen);
</script>
```



## 브랜드관 조회 측정

개별 브랜드관의 조회수를 측정하기 위해 **브랜드관 화면 내**에 API를 적용합니다. 아래 주의사항을 참고하여 적용해주세요.

* 브랜드관 메인(/initBrandCtg.siv)과 브랜드관 상세(/initBrandLowCtg.siv)에 모두 적용합니다.
* 카테고리 정보를 수집하는 코드는 브랜드관 상세에 적용하며 브랜드관 메인에는 적용하지 않습니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_brand";
	screen["page_id"] = "brand";
	screen["brand_name"] = "${brandName}";
	// 해당 브랜드의 명칭으로 치환하여 적용
	screen["category_id_a"] = "${categoryIdA}";
	screen["category_name_a"] = "${categoryNameA}";
	screen["category_id_b"] = "${categoryIdB}";
	screen["category_name_b"] = "${categoryNameB}";
	screen["category_id_c"] = "${categoryIdC}";
	screen["category_name_c"] = "${categoryNameC}";
	// 브랜드 상세 화면인 경우 해당 화면의 카테고리 대-중-소 정보를 치환하여 적용
	DOT.logScreen(screen);
</script>
```



### 적용예시

유저가 *STUDIO TOMBOY* 브랜드관에서 잡화 > 여성신발 > 샌들/슬리퍼 카테고리를 조회한 경우 해당 화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_brand";
	screen["page_id"] = "brand";
	screen["brand_name"] = "STUDIO TOMBOY";
	screen["category_id_a"] = "010000029585";
	screen["category_name_a"] = "잡화";
	screen["category_id_b"] = "010000029586";
	screen["category_name_b"] = "여성신발";
	screen["category_id_c"] = "010000029588";
	screen["category_name_c"] = "샌들/슬리퍼";
	DOT.logScreen(screen);
</script>
```



유저가 *STUDIO TOMBOY* 브랜드관 메인화면을 조회한 경우 해당 화면에 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_brand";
	screen["page_id"] = "brand";
	screen["brand_name"] = "STUDIO TOMBOY";
	/*
		브랜드 메인화면에는 카테고리 정보가 없으므로
		해당 정보를 수집하는 코드를 적용하지 않음
	
	screen["category_id_a"] = "${categoryIdA}";
	screen["category_name_a"] = "${categoryNameA}";
	screen["category_id_b"] = "${categoryIdB}";
	screen["category_name_b"] = "${categoryNameB}";
	screen["category_id_c"] = "${categoryIdC}";
	screen["category_name_c"] = "${categoryNameC}";
	*/
	DOT.logScreen(screen);
</script>
```



## 위시리스트 조회 측정

위시리스트 화면의 조회수를 측정하기 위해 **위시리스트 페이지 내**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_wishlist";
	screen["page_id"] = "wishlist";
	
	var product1 = new Object();
	product1["product_id"] = "${productId}";
	product1["product_name"] = "${productName}";
	product1["brand_name"] = "${brandName}";
	// 위시리스트 화면에 존재하는 상품의 코드, 명칭, 브랜드명으로 치환
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	// 위시리스트 화면에 존재하는 상품의 코드, 명칭, 브랜드명으로 치환
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
```



### 적용예시

*5AC 패밀리 백* 상품 1개가 위시리스트 화면 내에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_wishlist";
	screen["page_id"] = "wishlist";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	screen["product"] = product1;
	DOT.logScreen(screen);
</script>
```



*5AC 패밀리 백* 상품 1개와 *아쿠아 디 콜로니아 - 프리지아* 상품 2개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_wishlist";
	screen["page_id"] = "wishlist";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	var product2 = new Object();
	product2["product_id"] = "01P0000116871";
	product2["product_name"] = "아쿠아 디 콜로니아 - 프리지아";
	product2["brand_name"] = "SANTA MARIA NOBELLA";
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	screen["product"] = productArray;
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
	product1["brand_name"] = "${brandName}";
	// 쇼핑백 화면에 존재하는 상품의 코드, 명칭, 브랜드명으로 치환
	product1["quantity"] = ${quantity};
	
	var product2 = new Object();
	product2["product_id"] = "${productId}";
	product2["product_name"] = "${productName}";
	product2["brand_name"] = "${brandName}";
	// 쇼핑백 화면에 존재하는 코드, 명칭, 브랜드명으로 치환
	product2["quantity"] = ${quantity};
	
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
```



### 적용예시

*5AC 패밀리 백* 상품 1개가 쇼핑백 화면 내에 존재하는 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_cart";
	screen["page_id"] = "cart";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["quantity"] = 1;
	screen["product"] = product1;
	DOT.logScreen(screen);
</script>
```



*5AC 패밀리 백* 상품 1개와 *아쿠아 디 콜로니아 - 프리지아* 상품 2개가 구매 완료된 경우 아래와 같이 적용

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_cart";
	screen["page_id"] = "cart";
	var product1 = new Object();
	product1["product_id"] = "2005272626";
	product1["product_name"] = "5AC 패밀리 백";
	product1["brand_name"] = "MASION MARGIELA";
	product1["quantity"] = 2;
	var product2 = new Object();
	product2["product_id"] = "01P0000116871";
	product2["product_name"] = "아쿠아 디 콜로니아 - 프리지아";
	product2["brand_name"] = "SANTA MARIA NOBELLA";
	product2["quantity"] = 2;
	var productArray = new Array();
	productArray.push(product1);
	productArray.push(product2);
	screen["product"] = productArray;
	DOT.logScreen(screen);
</script>
```



## 메뉴 클릭 측정

아래 메뉴의 하위에 속한 주요 메뉴들의 클릭 수치를 측정하기 위해 API를 적용하게 됩니다.

1. header
2. GNB
3. 하단 bar
4. drawer (햄버거메뉴 클릭 후 펼쳐지는 화면 내에 있는 메뉴들)



클릭 측정 API를 적용할 대상 메뉴의 명칭, 위치는 아래 매핑 테이블을 참고하여 적용해 주시기 바랍니다.



### 매핑 테이블

| 번호 | 위치          | menuName           | 설명                                                         |
| :--: | ------------- | ------------------ | ------------------------------------------------------------ |
|  1   | header        | header_drawer      | 헤더에 있는 햄버거메뉴 버튼                                  |
|  2   | header        | header_search      | 헤더에 있는 돋보기 버튼                                      |
|  3   | header        | header_shoppingbag | 헤더에 있는 쇼핑백 버튼                                      |
|  4   | GNB           | gnb_home           | GNB에 있는 홈 메뉴탭<br />**스와이프로 홈화면이 열린 경우에도 API 호출** |
|  5   | GNB           | gnb_event          | GNB에 있는 이벤트 메뉴탭<br />**스와이프로 이벤트 화면이 열린 경우에도 API 호출** |
|  6   | GNB           | gnb_mgz            | GNB에 있는 매거진 메뉴탭<br />**스와이프로 매거진 화면이 열린 경우에도 API 호출** |
|  7   | GNB           | gnb_select         | GNB에 있는 셀렉트449 메뉴탭<br />**스와이프로 셀렉트449 화면이 열린 경우에도 API 호출** |
|  8   | GNB           | gnb_outlet         | GNB에 있는 아울렛 메뉴탭<br />**스와이프로 아울렛 화면이 열린 경우에도 API 호출** |
|  9   | bar           | bar_drawer         | 하단바에 있는 햄버거메뉴 버튼                                |
|  10  | bar           | bar_delivery       | 하단바에 있는 배송조회 버튼                                  |
|  11  | bar           | bar_home           | 하단바에 있는 홈버튼                                         |
|  12  | bar           | bar_mypage         | 하단바에 있는 마이페이지 버튼                                |
| 13 | bar | bar_rct_goods | 하단바에 있는 최근본상품 버튼 |
|  14  | drawer        | drawer_message     | 햄버거메뉴 내 메시지 버튼                                    |
|  15  | drawer        | drawer_setup       | 햄버거메뉴 내 설정 버튼                                      |
|  16  | drawer        | drawer_category    | 햄버거메뉴 내 카테고리탭                                     |
|  17  | drawer        | drawer_brand       | 햄버거메뉴 내 브랜드탭                                       |
|  18  | drawer        | drawer_allmenu     | 햄버거메뉴 내 전체메뉴탭                                     |
|  19  | drawer        | drawer_brand_navi  | 햄버거메뉴 내 브랜드 인덱스<br />**인덱스 zone 내에 있는 각 리스트가 클릭될때마다 API 호출** |
|  20  | drawer        | filter_select449   | 햄버거메뉴 내 브랜드탭 내 셀렉트449 탭<br />**해당 탭 클릭시 API 호출** |
|  21  | 검색결과 화면 | filter_select449   | 검색결과 화면 내 셀렉트449 탭<br />**해당 탭 클릭시 API 호출** |
|  22  | 카테고리 화면 | filter_select449   | 카테고리 화면 내 셀렉트449 탭<br />**해당 탭 클릭시 API 호출** |



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_click_menu";
	event["menu_name"] = "${menuName}";
	// 위 매핑 테이블 내 menuName 컬럼의 값으로 치환하여 적용
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 **헤더에 있는 쇼핑백 버튼을 클릭**한 경우 아래와 같이 적용

``` javascript
function menuClick() {
	var event = new Object();
	event["event"] = "w_click_menu";
	event["menu_name"] = "header_shoppingbag";
	DOT.logEvent(event);
}

onclick="menuClick()"
```



유저가 화면을 **스와이프하여 매거진 화면에 도달**한 경우 아래와 같이 적용

``` javascript
function menuClick() {
	var event = new Object();
	event["event"] = "w_click_menu";
	event["menu_name"] = "gnb_mgz";
	DOT.logEvent(event);
}

yourObject.on("swipe", menuClick);
```



유저가 검색결과 화면에서 셀렉트449 탭을 클릭한 경우 아래화 같이 적용

``` javascript
function menuClick() {
	var event = new Object();
	event["event"] = "w_click_menu";
	event["menu_name"] = "filter_select449";
	DOT.logEvent(event);
}

onclick="menuClick()"
```




## 배너 클릭 측정

아래에 리스팅한 *각 메인 화면* 내에 있는 배너에 대한 클릭을 의미합니다. 매핑 테이블에 정리된 **각 배너가 클릭된 시점**에 API를 적용해 주시기 바랍니다.

1. 홈
2. 기획전 메인
5. 아울렛 메인
4. 셀렉트449 메인
5. 개별 브랜드관
6. 개별 카테고리 메인



### 매핑 테이블

| 번호 | 위치                   | bannerName          | 설명                       |
| :--: | ---------------------- | ------------------- | -------------------------- |
|  1   | 홈                     | main_v              | 메인 비주얼 배너           |
|  2   | 홈                     | main_embed_a        | 메인 띠배너 (상단)         |
|  3   | 홈                     | main_thisweek       | 메인 This Week             |
|  4   | 홈                     | main_embed_b        | 메인 띠배너 (중단)         |
|  5   | 홈                     | main_whatsup        | 메인 Whats up              |
|  6   | 홈                     | main_embed_c        | 메인 띠배너 (하단)         |
|  7   | 기획전 메인            | shop_topbanner      | 기획전 탑배너              |
|  8   | 아울렛 메인            | outlet_topbanner    | 아울렛 탑배너              |
|  9   | 셀렉트449 메인         | select_topbanner    | 셀렉트449 탑배너           |
|  10  | 브랜드관               | brand_banner        | 브랜드관 탑배너            |
|  11  | 여성 카테고리          | ctg_women_banner    | 카테고리 여성배너          |
|  12  | 남성 카테고리          | ctg_men_banner      | 카테고리 남성배너          |
|  13  | 잡화 카테고리          | ctg_acc_banner      | 카테고리 잡화배너          |
|  14  | 아동 카테고리          | ctg_kids_banner     | 카테고리 아동배너          |
|  15  | 가구/인테리어 카테고리 | ctg_interior_banner | 카테고리 가구/인테리어배너 |
|  16  | 생활 카테고리          | ctg_living_banner   | 카테고리 생활배너          |



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_click_banner";
	event["banner_name"] = "${bannerName}";
	// 매핑 테이블을 참고하여 bannerName 을 치환하여 적용
	event["event_id"] = "${eventId}";
	event["event_name"] = "${eventName}";
	// 클릭된 배너가 이벤트 배너인 경우 해당 이벤트의 정보로 치환하여 적용
	event["shop_id] = "${shopId}";
	event["shop_name"] = "${shopName}";
	// 클릭된 배너가 기획전 배너인 경우 해당 기획전의 정보로 치환하여 적용
	event["placement"] = "${orderOfItem}";
	// 클릭된 아이템이 배치된 순서로 치환하여 적용, string type
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 **홈 화면의 메인 비주얼 배너 중 5번째에 배치**된 *잉크 S/S SEASON OFF* 를 클릭한 경우 아래와 같이 적용

``` javascript
function clickItem() {
	var event = new Object();
	event["event"] = "w_click_banner";
    event["banner_name"] = "main_v";
    /*
    	이벤트 배너가 아니므로 아래 코드는 적용하지 않음
    	
   		event["event_id"] = "${eventId}";
		event["event_name"] = "${eventName}";
	
	*/
	event["shop_id"] = "2003014479";
	event["shop_name"] = "잉크 S/S SEASON OFF";
	event["placement"] = "5";
	DOT.logEvent(event);
}

onclick="clickItem()"
```



## 아이템 클릭 측정

'아이템'이란 아래 리스팅한 화면 내에 배치된 '상품'과 홈화면에 있는 '카테고리 아이콘' + '키워드'에 대한 클릭을 의미합니다. 아래 매핑 테이블을 참고하여 각 영역에 있는 **상품이 클릭된 시점**에 API를 적용해 주시기 바랍니다.

1. 홈 화면
2. 상품 상세 화면
3. 기획전 상세 화면
4. 이벤트 상세 화면
5. 매거진 상세 화면
6. 브랜드관 화면



### 매핑 테이블

| 번호 | 영역            | itemType         | 비고 |
| :--: | --------------- | ---------------- | |
|  1   | 홈 베스트상품   | main_item_best   | |
|  2   | 홈 신상품       | main_item_new    | |
|  3   | 홈 에디터초이스 | main_item_editor | |
|  4   | 홈 핫브랜드     | main_brand       | |
|  5   | 홈 카테고리아이콘     | main_ctg_icon  | |
|  6   | 홈 키워드     | main_keyword       | |
|  7   | 상품 상세     | goods_rcm       | 함께 많이 본 상품, 카테고리 구매 베스트, 함께 구매하면 좋은 상품 모두 적용 |
|  8   | 기획전 상세     | shop_goods       | |
|  9   | 이벤트 상세     | event_goods       | |
| 10 | 매거진 상세 | scrat_goods | |
| 11 | 브랜드관 | brand_goods | |



### 측정 API


``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_click_item";
	event["item_type"] = "${itemType}";
	// 매핑 테이블을 참고하여 itemType 을 치환
	event["item_name"] = "${itemName}";
	// 클릭된 항목의 명칭으로 itemName 을 치환 (상품명, 아이콘명, 키워드)
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 홈화면의 신상품 영역에서 *하이넥 플리츠 실크 블라우스* 상품을 클릭한 경우 아래와 같이 적용

```javascript
function itemClick() {
	var event = new Object();
	event["event"] = "w_click_item";
	event["item_type"] = "main_item_new";
	event["item_name"] = "하이넥 플리츠 실크 블라우스";
	DOT.logEvent(event);
}

onclick="itemClick()"
```



유저가 홈화면의 카테고리 아이콘 영역에서 *잡화* 버튼을 클릭한 경우 아래와 같이 적용

```javascript
function itemClick() {
	var event = new Object();
	event["event"] = "w_click_item";
	event["item_type"] = "main_ctg_icon";
	event["item_name"] = "잡화";
	DOT.logEvent(event);
}

onclick="itemClick()"
```



유저가 상품 상세 화면의 함께 많이 본 상품 영역에서 *콜렌 플리츠 하프 팬츠* 상품을 클릭한 경우 아래와 같이 적용

```javascript
function itemClick() {
	var event = new Object();
	event["event"] = "w_click_item";
	event["item_type"] = "goods_rcm";
	event["item_name"] = "콜렌 플리츠 하프 팬츠";
	DOT.logEvent(event);
}

onclick="itemClick()"
```



## 팝업 클릭 측정

메인 화면에 노출하는 팝업 레이어의 클릭수를 측정하기 위해 **팝업 클릭 시점**에 API를 적용합니다.



### 측정 API

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "w_click_popup";
	event["popup_name"] = "${popupName}";
	event["placement"] = "${orderOfItem}"; // string
	event["event_id"] = "${eventId}";
	event["event_name"] = "${eventName}";
	event["shop_id"] = "${shopId}";
	event["shop_name"] = "${shopName}";
	DOT.logEvent(event);
</script>
```



### 적용예시

유저가 팝업의 두 번째 슬라이드에 배치된 *나만 알고 있었던 SI 뷰티 인생템* 배너를 클릭한 경우 아래와 같이 적용

``` javascript
function popupClick() {
	var event = new Object();
	event["event"] = "w_click_popup";
	event["popup_name"] = "나만 알고 있었던 SI 뷰티 인생템";
	event["placement"] = "2";
	/* 
	기획전인 경우 이벤트 정보 수집용 코드는 적용하지 않음
	
	event["event_id"] = "${eventId}";
	event["event_name"] = "${eventName}";
	*/
	event["shop_id"] = "2007019775";
	event["shop_name"] = "나만 알고 있었던 SI 뷰티 인생템";
	DOT.logEvent(event);
}

onclick="popupClick()"
```



## 재입고 알림신청 측정

품절된 상품에 대한 ''재입고 알림신청' 버튼의 클릭 횟수를 측정하기 위해 **해당 버튼이 클릭되는 시점**에 API를 적용힙니다.

* 알림신청 완료가 아닌 *해당 버튼의 클릭 시점*에 적용해 주시기 바랍니다.



### 측정 API

```javascript
var event = new Object();
event["event"] = "notice_instock";
event["g103"] = 1;
var product = new Object();
product["product_id"] = "${productId}";
product["product_name"] = "${productName}";
product["brand_name"] = "${brandName}";
// 버튼이 클릭된 상품의 코드, 명칭, 브랜드 정보로 치환하여 적용
event["product"] = product;
DOT.logEvent(event);
```



## 적용예시

*탑 스티치 히든 벨티드 코드* 상품 상세화면에서 ''재입고 알림신청' 버튼이 클릭된 경우 아래와 같이 적용

```javascript
function reStockClick() {
	var event = new Object();
	event["event"] = "notice_instock";
	event["g103"] = 1;
    var product = new Object();
	product["product_id"] = "1912230695";
	product["product_name"] = "탑 스티치 히든 벨티드 코드";
	product["brand_name"] = "MARNI";
    event["product"] = product;
	DOT.logEvent(event);
}

onclick="reStockClick()"
```



## App Push 동의 여부 측정

유저가 App Push에 대해 동의 또는 비동의 하는 횟수를 측정하기 위해 API를 적용합니다. 유저가 **동의 또는 비동의한 시점**에 API를 적용해주세요. 아래 리스팅한 경우를 포함하여, 앱 푸시 동의/비동의가 변경되는 모든 펑션에 본 API가 적용되어야 합니다.

* SIV 앱의 '설정 > 쇼핑혜택 알림 받기'에 체크하는 것에 따라 동의/비동의가 변경



### 측정 API

``` javascript
DOT.setUser(User.setAttr3("${attr3Code}"));
/*
	유저가 동의한 경우 opt-in
	유저가 비동의한 경우 opt-out
	
	동의 여부에 따라 attr3Code를 위 값으로 치환하여 적용
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

유저가 '쇼핑혜택 알림 받기'에 체크표시를 하여 App Push 수신에 동의한 경우 아래와 같이 적용

``` javascript
function appPushChk() {
	alert("알림 수신이 설정되었습니다. (전송자: 신세계인터내셔날)");
    
	DOT.setUser(User.setAttr3("opt-in"));
	var event = new Object();
	event["event"] = "w_notification_opt_in";
	DOT.logEvent(event);
}
```



## 쿠폰 다운로드 측정

쿠폰이 다운로드된 횟수를 측정하기 위해 정상적으로 **쿠폰 다운로드가 완료된 시점**에 API를 적용합니다.

* 마이 페이지의 '쿠폰' 메뉴에서 *쿠폰 한번에 받기* 또는 개별 쿠폰의 *다운로드 버튼을 클릭* 하는 경우
* 상품 상세 페이지에서 쿠폰을 다운로드 하는 경우
* 쇼핑백 페이지에서 쿠폰을 다운로드 하는 경우
* 앱 다운로드 이벤트에서 앱 전용 쿠폰을 다운로드 하는 경우



등 쿠폰의 종류와 관계 없이 쿠폰 다운로드가 완료될때마다 API를 호출하면 됩니다.



### 측정 API & 적용예시

``` javascript
function cpnDown() {
	...
	alert("쿠폰을 다운로드 하였습니다.");
	var event = new Object();
	event["event"] = "w_download_coupon";
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
