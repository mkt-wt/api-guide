# Wisetracker Integration Guide
'MyNB'앱의 데이터 분석을 위해 적용이 필요한 아래 사항들을 안내하는 기술 문서입니다.

1. iOS의 Universal Link 설정 적용
2. 와이즈트래커 2.0 버전 추가 적용
3. 모바일 웹사이트 상에 컨버전 트래킹용 스크립트 적용



적용 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr



# Index
* [Universal Link 설정](./mynb_2.0.md#Universal-Link-설정)
* [와이즈트래커 2.0 SDK 추가](./mynb_2.0.md#와이즈트래커-20-SDK-추가)
* [인앱 이벤트 API 추가](./mynb_2.0.md#인앱-이벤트-API-추가)
	* [구매](./mynb_2.0.md#구매)
	* [로그인](./mynb_2.0.md#로그인)
	* [회원가입](./mynb_2.0.md#회원가입)
	* [하단 탭바 클릭 측정](./mynb_2.0.md#메뉴-클릭-측정)
	* [Home 화면의 배너 클릭 측정](./mynb_2.0.md#Home-화면의-배너-클릭-측정)
	* [이벤트 상세화면 내의 버튼 클릭 측정](./mynb_2.0.md#이벤트-상세화면-내의-버튼-클릭-측정)
	* [포스트 상세화면 내의 버튼 클릭 측정](./mynb_2.0.md#포스트-상세화면-내의-버튼-클릭-측정)
	* [포스트 상세화면 내의 상품 클릭 측정](./mynb_2.0.md#포스트-상세화면-내의-상품-클릭-측정)
	* [포스트 상세화면 내의 관심상품 등록 측정](./mynb_2.0.md#포스트-상세화면-내의-관심상품-등록-측정)
	* [투데이 아이템 클릭 측정](./mynb_2.0.md#투데이-아이템-클릭-측정)
	* [퀴즈 상세화면 내의 랜딩버튼 클릭 측정](./mynb_2.0.md#퀴즈-상세화면-내의-랜딩버튼-클릭-측정)
	* [포인트 사용 완료 측정](./mynb_2.0.md#포인트-사용-완료-측정)
	* [기부 완료 측정](./mynb_2.0.md#기부-완료-측정)
	* [스트라바 포인트 전환 완료 측정](./mynb_2.0.md#스트라바-포인트-전환-완료-측정)
	* [우먼스 클래스 & 우먼스클래스 이용권 신청하기 측정](./mynb_2.0.md#우먼스-클래스--우먼스클래스-이용권-신청하기-측정)
	* [우먼스 클래스 & 우먼스클래스 이용권 공유하기 측정](./mynb_2.0.md#우먼스-클래스--우먼스클래스-이용권-공유하기-측정)
* [화면별 페이지뷰 측정용 API 추가](./mynb_2.0.md#화면별-페이지뷰-측정용-API-추가)
	* [매핑 테이블](./mynb_2.0.md#매핑-테이블-1)
	* [상품 화면](./mynb_2.0.md#상품-화면)
	* [로그인 화면](./mynb_2.0.md#로그인-화면---Hybrid)
	* [회원가입 화면](./mynb_2.0.md#회원가입-화면---Hybrid)
	* [포인트 화면](./mynb_2.0.md#포인트-화면---Hybrid)
	* [퀴즈 상세 화면](./mynb_2.0.md#퀴즈-상세-화면---Hybrid)
	* [기부 캠페인 상세 화면](./mynb_2.0.md#기부-캠페인-상세-화면---Hybrid)
	* [포스트 리스트 화면](./mynb_2.0.md#포스트-리스트-화면---Hybrid)
	* [포스트 상세 화면](./mynb_2.0.md#포스트-상세-화면---Hybrid)
	* [이벤트 리스트 화면](./mynb_2.0.md#이벤트-리스트-화면---Hybrid)
	* [이벤트 상세 화면](./mynb_2.0.md#이벤트-상세-화면---Hybrid)
	* [스포츠 화면](./mynb_2.0.md#스포츠-화면---Hybrid)
	* [메뉴 화면](./mynb_2.0.md#메뉴-화면---Hybrid)
	* [기타 화면](./mynb_2.0.md#기타-화면---Hybrid)
	* [네이티브 화면](./mynb_2.0.md#네이티브-화면)
* [웹 컨버전 스크립트 추가](./mynb_2.0.md#웹-컨버전-스크립트-추가)
  * [웹 SDK 추가](./mynb_2.0.md#웹-SDK-추가)
  * [구매 측정](./mynb_2.0.md#구매-측정)



## Universal Link 설정

[Universal Link](https://developer.apple.com/ios/universal-links/)는 iOS 플랫폼에서 웹과 앱 사이의 자연스러운 연결을 제공하는 Deep Linking 규격입니다. MyNB iOS 앱에 Univesal Link를 적용하기 위해 아래 설정을 추가해 주시기 바랍니다.

* [Univesal Link 온라인 가이드](http://document.wisetracker.co.kr/v1/docs/sdk/ios/ios-install-guide#22-univarsal-link-%EB%B6%84%EC%84%9D-%EC%A0%81%EC%9A%A9)



## 와이즈트래커 2.0 SDK 추가

현재 MyNB 앱에는 와이즈트래커 1.0 버전의 SDK와 API들이 적용되어 있으며, 기 적용된 1.0을 제거하지 않고 새롭게 2.0 버전을 추가 적용 해야 합니다. 아래 가이드를 참고하여 2.0 버전의 SDK를 적용해 주시기 바랍니다.

* [Android SDK](http://document.wisetracker.co.kr/v2/docs/sdk/android/android-install-guide)
* [iOS SDK](http://document.wisetracker.co.kr/v2/docs/sdk/ios/ios-install-guide)



## 인앱 이벤트 API 추가

유저가 앱 내에서 발생시킨 행동을 *인앱 이벤트* 라고 부르며 인앱 이벤트 API는 발생한 인앱 이벤트를 측정하는 역할을 합니다. 아래 내용을 참고하여 API를 적용해 주시기 바랍니다.



### 구매

유저가 우먼스 클래스, 우먼스 클래스 이용권, NBRC에 대해 비용을 지불하는 것을 '구매'로 간주합니다. 구매 완료 화면에 아래 코드를 추가해 주세요.



#### 주의사항

구매 완료 화면에 기 적용된 와이즈트래커 코드가 있을 것입니다. 해당 코드를 아래 내용으로 업데이트 해주시기 바랍니다.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setOrderProductArray(["상품ID"]);
	WiseTracker.setOrderQuantityArray([구매수량]); // float
	WiseTracker.setOrderAmountArray([구매금액]); // float
	WiseTracker.setOrderNo("주문번호");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var purchase = new Object(); 
	purchase["ordNo"] = "주문번호";
	purchase["curcy"] = "KRW";
	var product1 = new Object();
	product1["pnc"] = "상품ID";
	product1["pncNm"] = "상품명";
	product1["amt"] = 구매금액; // float
	product1["ea"] = 구매수량; // float
	var productArray = new Array();
	productArray.push(product1);
	purchase["product"] = productArray;
	DOT.logPurchase(purchase);
</script>
```



#### 적용예시

*NB 우먼스 클래스 3개월 패키지* 상품을 구매한 경우 구매 완료 화면에 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["asdf123"]);
	WiseTracker.setOrderQuantityArray([1]);
	WiseTracker.setOrderAmountArray([550000]);
	WiseTracker.setOrderNo("tr012345");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var purchase = new Object(); 
	purchase["ordNo"] = "tr012345";
	purchase["curcy"] = "KRW";
	var product1 = new Object();
	product1["pnc"] = "asdf123";
	product1["pncNm"] = "NB 우먼스 클래스 3개월 패키지";
	product1["amt"] = 550000;
	product1["ea"] = 1;
	var productArray = new Array();
	productArray.push(product1);
	purchase["product"] = productArray;
	DOT.logPurchase(purchase);
</script>
```



### 로그인

앱에서 로그인이 완료되는 시점에 아래 코드를 추가해 주세요.



#### 주의사항

로그인한 유저의 성별과 연령대 정보를 함께 수집하는데, 이에 사용하는 value는 아래에 있는 매핑 테이블에 명시한 것을 사용해 주세요.



#### 매핑 테이블

로그인한 유저의 **성별**은 아래 value로 설정해 주시기 바랍니다.

| 성별 | value |
| --- | --- |
| 남성 | male |
| 여성 | female |
| 기타 (남성 또는 여성이 아닌 모든 경우) | non avaliable |

로그인한 유저의 **연령대**는 아래 value로 설정해 주시기 바랍니다.

| 연령대 | value |
| --- | --- |
| 10세 미만 | under 10s |
| 10대 | 10s |
| 20대 | 20s |
| 30대 | 30s |
| 40대 | 40s |
| 50대 | 50s |
| 60대 | 60s |
| 60대 이상 | over 60s |
| 기타 | non avaliable |

로그인한 유저의 로그인 유형은 아래 value로 설정해 주시기 바랍니다.

| 로그인 유형 | value |
| --- | --- |
| MyNB 계정 | NB_account |
| 카카오 | kakao |
| 네이버 | naver |



#### 측정 API

**Android**

``` java
User user = new User.Builder()
		.setGender("성별")
		.setAge("연령대")
		.build();
DOT.setUser(user); //유저 정보 측정

Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "login_complete");
eventMap.put("loginTp", "로그인 유형");
DOT.logEvent(eventMap); //로그인 이벤트 측정
```



**iOS - Swift**

``` swift
DOT.setUser(
	User.builder({ (builder) in
		let user = builder as! User
		user.gender = "성별"
		user.age = "연령대"
	})
)

let event = NSMutableDictionary()
event["event"] = "login_complete"
event["loginTp"] = "로그인 유형"
DOT.logEvent(event) //로그인 이벤트 측정
```



**Hybrid**

``` html
<script type="text/javascript">
	DOT.setUser(User.setGender("성별")
	.setAge("연령대")); //유저 정보 측정

	var event = new Object(); 
	event["event"] = "login_complete";
	event["loginTp"] = "로그인 유형";
	DOT.logEvent(event); //로그인 이벤트 측정
</script>
```



#### 적용예시

카카오 계정으로 로그인한 유저가 20대 여성인 경우 아래와 같이 적용

**Android**

``` java
User user = new User.Builder()
		.setGender("female") //매핑 테이블 참고
		.setAge("20s") //매핑 테이블 참고
		.build();
DOT.setUser(user);

Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "login_complete");
eventMap.put("loginTp", "kakao"); //매핑 테이블 참고
DOT.logEvent(eventMap);
```


**iOS - Swift**

``` swift
DOT.setUser(
	User.builder({ (builder) in
		let user = builder as! User
		user.gender = "female" //매핑 테이블 참고
		user.age = "20s" //매핑 테이블 참고
	})
)

let event = NSMutableDictionary()
event["event"] = "login_complete"
event["loginTp"] = "kakao" //매핑 테이블 참고
DOT.logEvent(event)
```



**Hybrid**

``` html
<script type="text/javascript">
	DOT.setUser(User.setGender("female") //매핑 테이블 참고
		.setAge("20s")); //매핑 테이블 참고
			
	var event = new Object();
	event["event"] = "login_complete";
	event["loginTp"] = "kakao" //매핑 테이블 참고
	DOT.logEvent(event);
</script>
```



### 회원가입

앱에서 회원가입이 완료되는 시점(회원가입 완료 화면 권장)에 아래 코드를 추가해 주세요.



#### 주의사항

어떤 유형으로 회원가입 했는지에 대해 정보를 수집하는데, 이에 사용하는 value는 아래에 있는 매핑 테이블에 명시한 것을 사용해 주세요.



#### 매핑 테이블

가입한 유저의 **가입 유형**은 아래 value로 설정해 주시기 바랍니다.

| 가입 유형 | value      |
| --------- | ---------- |
| MyNB 계정 | NB_account |
| 카카오    | kakao      |
| 네이버    | naver      |



#### 측정 API

**Hybrid**

``` html
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var event = new Object();
	event["event"] = "signup_complete";
	event["signupTp"] = "가입유형";
	DOT.logEvent(event);
</script>
```



#### 적용예시

MyNB 계정으로 가입한 경우 아래와 같이 적용

**Hybrid**

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "signup_complete";
	event["signupTp"] = "NB_account"; // 매핑 테이블 참고
	DOT.logEvent(event);
</script>
```



네이버 계정으로 가입한 경우 아래와 같이 적용

**Hybrid**

``` html
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "signup_complete";
	event["signupTp"] = "naver"; // 매핑 테이블 참고
	DOT.logEvent(event);
</script>
```



### 메뉴 클릭 측정

앱 하단에 위치한 메뉴바 & 홈화면 중간에 있는 탭메뉴가 클릭되는 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Android**

``` java
//V1
WiseTracker.sendClickData("EVT", "메뉴_메뉴명칭");
// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요


//V2
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "click_menu");
eventMap.put("menu_name", "메뉴명칭");
// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요
DOT.logEvent(eventMap);
```


**iOS - Swift**

``` swift
//V1
WiseTracker.sendClickData("EVT", eventName: "메뉴_메뉴명칭")
// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요


//V2
let event = NSMutableDictionary()
event["event"] = "click_menu"
event["menu_name"] = "메뉴명칭"
// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요
DOT.logEvent(event)
```



**Hybrid**

``` html
//V1
<script type="text/javascript">
	WiseTracker.sendClickData("EVT", eventName: "메뉴_메뉴명칭")
	// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요
</script>


//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "click_menu";
	event["menu_name"] = "메뉴명칭";
	// '메뉴명칭' 부분은 실제 클릭된 메뉴명칭으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시 1

유저가 하단 메뉴바에서 'NB PLAY'를 클릭한 경우 다음과 같이 적용



**Android**

``` java
//V1
WiseTracker.sendClickData("EVT", "메뉴_NBPLAY");


//V2
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "click_menu");
eventMap.put("menu_name", "NBPLAY");
DOT.logEvent(eventMap);
```


**iOS - Swift**

``` swift
//V1
WiseTracker.sendClickData("EVT", eventName: "메뉴_NBPLAY")

//V2
let event = NSMutableDictionary()
event["event"] = "click_menu"
event["menu_name"] = "NBPLAY"
DOT.logEvent(event)
```



#### 적용예시 2

유저가 홈화면 중간에 있는 탭메뉴에서 'Ranking'을 클릭한 경우 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="text/javascript">
	WiseTracker.sendClickData("EVT", eventName: "메뉴_Ranking");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "click_menu";
	event["menu_name"] = "Ranking";
	DOT.logEvent(event);
</script>
```



### Home 화면의 배너 클릭 측정

앱의 Home 화면에 배치된 배너들이 클릭되는 시점에 아래 코드를 추가해 주세요.



#### 주의사항

유저가 클릭한 배너의 명칭과 해당 배너의 배치 순서를 value에 넣어야 합니다. 적용예시를 참고하여 작업해 주세요.



#### 측정 API

**Android**

``` java
//V1
WiseTracker.sendClickData("EVT", "HOME_타입_배너명칭");
// '타입' 부분은 클릭된 배너의 위치에 따라 '상단배너' 또는 '기획전배너'로 replace 필요
// '배너명칭' 부분은 실제 배너명칭으로 replace 필요


//V2
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "click_banner");
eventMap.put("banner_name", "배너명칭");
// '배너명칭' 부분은 실제 배너명칭으로 replace 필요
eventMap.put("contents_path", "home^타입^배너명칭");
// value의 ^ 기호는 와이즈트래커에서 사용하는 구분자
// '타입' 부분은 클릭된 배너의 위치에 따라 '상단배너' 또는 '기획전배너'로 replace 필요
// '배너명칭' 부분은 실제 배너명칭으로 replace 필요
DOT.logEvent(eventMap);
```

**iOS - Swift**

``` swift
//V1
WiseTracker.sendClickData("EVT", eventName: "HOME_타입_배너명칭")
// '타입' 부분은 클릭된 배너의 위치에 따라 '상단배너' 또는 '기획전배너'로 replace 필요
// '배너명칭' 부분은 실제 배너명칭으로 replace 필요


//V2
let event = NSMutableDictionary()
event["event"] = "click_banner"
event["banner_name"] = "배너명칭"
event["contents_path"] = "home^타입^배너명칭"
// value의 ^ 기호는 와이즈트래커에서 사용하는 구분자
// '타입' 부분은 클릭된 배너의 위치에 따라 '상단배너' 또는 '기획전배너'로 replace 필요
// '배너명칭' 부분은 실제 배너명칭으로 replace 필요
DOT.logEvent(event)
```



#### 적용예시

유저가 홈화면 상단에 있는 'N-CLAY로 즐거운 여름 만들기' 배너를 클릭한 경우 다음과 같이 적용



**Android**

``` java
//V1
WiseTracker.sendClickData("EVT", "HOME_상단배너_N-CLAY로 즐거운 여름 만들기");


//V2
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "click_banner");
eventMap.put("banner_name", "N-CLAY로 즐거운 여름 만들기");
eventMap.put("contents_path", "home^상단배너^N-CLAY로 즐거운 여름 만들기");
DOT.logEvent(eventMap);
```

**iOS - Swift**

``` swift
//V1
WiseTracker.sendClickData("EVT", eventName: "HOME_상단배너_N-CLAY로 즐거운 여름 만들기")


//V2
let event = NSMutableDictionary()
event["event"] = "click_banner"
event["banner_name"] = "N-CLAY로 즐거운 여름 만들기"
event["contents_path"] = "home^상단배너^N-CLAY로 즐거운 여름 만들기"
DOT.logEvent(event);
```



### 이벤트 상세화면 내의 버튼 클릭 측정

개별 이벤트 상세화면에 있는 다음 세 가지 버튼이 클릭되는 시점에 아래 코드를 추가해 주세요.

* 좋아요 버튼
* 공유 버튼 
* 온라인샵 랜딩버튼



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "EVENT_이벤트제목_버튼명칭");
	// '이벤트제목' 부분은 실제 이벤트 제목으로 replace 필요
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '좋아요', '공유', '랜딩버튼'으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "click_button";
	event["button_name"] = "버튼명칭";
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '좋아요', '공유', '랜딩버튼'으로 replace 필요
	event["event_name"] = "이벤트제목";
	// '이벤트제목'부분은 실제 이벤트 제목으로 replace 필요
	event["contents_path"] = "event^이벤트제목^버튼명칭";
	// value의 ^ 기호는 와이즈트래커에서 사용하는 구분자
	// '이벤트제목' 부분은 실제 이벤트 제목으로 replace 필요
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '좋아요', '공유', '랜딩버튼'으로 replace 필요
	DOT.logEvent(event);
</script>
```

#### 적용예시

유저가 '맴버스위크 My Pick 이벤트' 이벤트의 좋아요 버튼을 클릭한 경우 다음과 같이 적용



**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "EVENT_맴버스위크 My Pick 이벤트_좋아요");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "click_button"
	event["button_name"] = "좋아요";
	event["event_name"] = "맴버스위크 My Pick 이벤트";
	event["contents_path"] = "event^맴버스위크 My Pick 이벤트^좋아요";
	DOT.logEvent(event);
</script>
```



### 포스트 상세화면 내의 버튼 클릭 측정

개별 포스트 상세화면에 있는 다음 두 가지 버튼이 클릭되는 시점에 아래 코드를 추가해 주세요.

* 유튜브 조회 (영상 내의 재생버튼이 아닌, 영상 제목을 클릭했을때 앱 내에서 새 창으로 열리게 하는 버튼)
* 온라인샵 랜딩버튼



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_포스트제목_버튼명칭");
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '유튜브조회', '랜딩버튼'으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "click_button";
	event["button_name"] = "버튼명칭";
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '유튜브조회', '랜딩버튼'으로 replace 필요
	event["content_name"] = "포스트제목";
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	event["contents_path"] = "post^포스트제목^버튼명칭";
	// value의 ^ 기호는 와이즈트래커에서 사용하는 구분자
	// '포스트제목' 부분은 실제 이벤트 제목으로 replace 필요
	// '버튼명칭' 부분은 클릭된 버튼에 따라 '유튜브조회', '랜딩버튼'으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

유저가 *MS327 Review* 포스트에서 '런칭 캘린터 바로가기' 버튼(온라인샵 랜딩버튼)을 클릭한 경우 다음과 같이 적용



**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_MS327 Review_랜딩버튼");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "click_button";
	event["button_name"] = "랜딩버튼";
	event["content_name"] = "MS327 Review";
	event["contents_path"] = "post^MS327 Review^랜딩버튼";
	DOT.logEvent(event);
</script>
```



### 포스트 상세화면 내의 상품 클릭 측정

개별 포스트 상세화면에 상품을 노출된 상품을 클릭한 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_포스트제목_상품클릭");
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "click_item";
	event["item_name"] = "아이템명";
	// '아이템명'은 클릭된 상품의 상품명으로 replace 필요
	event["content_name"] = "포스트제목";
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	event["contents_path"] = "post^포스트제목^상품클릭";
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

유저가 *Short Sleeve, Short Summer* 포스트에서 'UNI 데이지팩 등판 데이지 반팔티' 상품을 클릭한 경우 다음과 같이 적용



**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_Short Sleeve, Short Summer_상품클릭");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "click_item";
	event["item_name"] = "UNI 데이지팩 등판 데이지 반팔티";
	event["content_name"] = "Short Sleeve, Short Summer";
	event["contents_path"] = "post^Short Sleeve, Short Summer^상품클릭";
	DOT.logEvent(event);
</script>
```



### 포스트 상세화면 내의 관심상품 등록 측정

개별 포스트 상세화면에 상품을 노출된 상품 옆에 있는 하트버튼을 클릭하여, 해당 상품이 관심상품으로 등록 완료된 시점에 아래 코드를 추가해 주세요. 하트버튼을 다시 클릭해 등록을 해제한 경우에는 아래 코드가 읽혀서는 안됩니다.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_포스트제목_관심상품등록");
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "add_to_wishlist";
	event["item_name"] = "아이템명";
	// '아이템명'은 위시리스트에 등록된 상품의 상품명으로 replace 필요
	event["content_name"] = "포스트제목";
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	event["contents_path"] = "post^포스트제목^관심상품등록";
	// '포스트제목' 부분은 실제 포스트의 제목으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

유저가 *불쾌지수를 낮추는 가장 부드러운 방법* 포스트에서 'NB X T&T FLIPFLOP / SD5601GBK' 상품을 관심상품으로 등록한 경우 다음과 같이 적용



**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POST_불쾌지수를 낮추는 가장 부드러운 방법_관심상품등록");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "add_to_wishlist";
	event["item_name"] = "NB X T&T FLIPFLOP / SD5601GBK";
	event["content_name"] = "불쾌지수를 낮추는 가장 부드러운 방법";
	event["contents_path"] = "post^불쾌지수를 낮추는 가장 부드러운 방법^관심상품등록";
	DOT.logEvent(event);
</script>
```



### 투데이 아이템 클릭 측정

Point 탭에 있는 투데아아이템의 '상품 보러 가기' 버튼이 클릭되는 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_투데이아이템");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "click_item";
	event["item_name"] = "[투데이아이템] 아이템명";
	// '아이템명'은 클릭된 상품의 상품명으로 replace 필요
	// '[투데이아이템]'은 prefix의 역할을 하며 고정값임
	event["contents_path"] = "points^투데이아이템^상품명";
	// '상품명' 부분은 실제 상품의 명칭으로 replace 필요
	DOT.logEvent(event);
</script>
```



### 퀴즈 상세화면 내의 랜딩버튼 클릭 측정

퀴즈 상세화면에 있는 랜딩버튼이 클릭된 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_퀴즈명_랜딩버튼");
	// '퀴즈명' 부분은 실제 퀴즈의 제목으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "click_button";
	event["button_name"] = "랜딩버튼";
	event["serise_name"] = "퀴즈명";
	// '퀴즈명' 부분은 실제 퀴즈의 제목으로 replace 필요
	event["contents_path"] = "points^퀴즈명^랜딩버튼";
	// '퀴즈명' 부분은 실제 상품의 명칭으로 replace 필요
	DOT.logEvent(event);
</script>
```



### 포인트 사용 완료 측정

포인트를 사용하는 다음 두 가지 행동이 정상적으로 완료된 시점에 아래 코드를 추가해 주세요.

* 상품 쿠폰 전환 완료
* 액티비티 쿠폰 전환 완료



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_전환완료_전환타입");
	// '전환타입' 부분은 '상품쿠폰', '액티비티쿠폰' 둘 중 하나로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "use_credit";
	event["credit_name"] = "전환타입";
	// '전환타입' 부분은 '상품쿠폰', '액티비티쿠폰' 둘 중 하나로 replace 필요
	// '쿠폰금액' 부분은 상품 또는 액티비티 쿠폰의 금액(1만원, 2만원 등)으로 replace 필요
	event["g2"] = 쿠폰금액; // float
	// '쿠폰금액' 부분은 상품 또는 액티비티 쿠폰의 금액(1만원, 2만원 등)으로 replace 필요
	event["contents_path"] = "points^전환타입^쿠폰금액";
	// value의 ^ 기호는 와이즈트래커에서 사용하는 구분자
	// '전환타입' 부분은 '상품쿠폰', '액티비티쿠폰' 둘 중 하나로 replace 필요
	// '쿠폰금액' 부분은 상품 또는 액티비티 쿠폰의 금액(10000, 20000)으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

유저가 3만원 상품 쿠폰을 전환 완료한 경우 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_전환완료_상품쿠폰");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "use_credit";
	event["credit_name"] = "상품쿠폰";
	event["g2"] = 30000;
	event["contents_path"] = "points^상품쿠폰^30000";
	DOT.logEvent(event);
</script>
```



### 기부 완료 측정

기부가 정상적으로 완료된 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_기부_캠페인명");
	// '캠페인명' 부분은 실제 기부캠페인의 제목으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "donation_complete";
	event["campaign_name"] = "캠페인명";
	// '캠페인명' 부분은 실제 기부캠페인의 제목으로 replace 필요
	event["contents_path"] = "points^기부^캠페인명";
	// '캠페인명' 부분은 실제 기부캠페인의 제목으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

유저가 *혼자가 아닌 우리의 힘으로, 리커버리 야구단* 캠페인에 기부를 완료한 경우 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "POINTS_기부_혼자가 아닌 우리의 힘으로, 리커버리 야구단");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "donation_complete";
	event["campaign_name"] = "혼자가 아닌 우리의 힘으로, 리커버리 야구단";
	event["contents_path"] = "points^기부^혼자가 아닌 우리의 힘으로, 리커버리 야구단";
	DOT.logEvent(event);
</script>
```



### 스트라바 포인트 전환 완료 측정

스트라바의 포인트 전환이 정상적으로 완료된 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "SPORTS_스트라바_전환완료");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "use_credit";
	event["credit_name"] = "strava";
	event["contents_path"] = "sports^스트라바^전환완료";
	DOT.logEvent(event);
</script>
```



### 우먼스 클래스 & 우먼스클래스 이용권 신청하기 측정

우먼스 클래스와 우먼스 클래스 이용권 화면에 있는 신청하기 버튼이 클릭되는 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "SPORTS_상품명_신청하기");
	// '상품명' 부분은 클릭된 상품의 상품명으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "checkout";
	event["pnc"] = "상품ID";
	// 클릭된 상품의 상품ID로 replace 필요
	event["pncNm"] = "상품명";
	// 클릭된 상품의 상품명으로 replace 필요
	event["contents_path"] = "sports^상품명^신청하기";
	// '상품명' 부분은 클릭된 상품의 상품명으로 replace 필요
	DOT.logEvent(event);
</script>
```



#### 적용예시

*한강 피크닉_SUP WORKOUT* 클래스의 신청하기 버튼을 클릭한 경우 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "SPORTS_한강 피크닉_SUP WORKOUT_신청하기");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "checkout";
	event["pnc"] = "qwer123";
	event["pncNm"] = "한강 피크닉_SUP WORKOUT";
	event["contents_path"] = "sports^한강 피크닉_SUP WORKOUT^신청하기";
	DOT.logEvent(event);
</script>
```



### 우먼스 클래스 & 우먼스클래스 이용권 공유하기 측정

우먼스 클래스와 우먼스 클래스 이용권 화면에 있는 공유하기 버튼이 클릭되는 시점에 아래 코드를 추가해 주세요.



#### 측정 API

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "SPORTS_상품명_공유");
	// '상품명' 부분은 클릭된 상품의 상품명으로 replace 필요
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object(); 
	event["event"] = "share";
	event["pnc"] = "상품ID";
	// 클릭된 상품의 상품ID로 replace 필요
	event["pncNm"] = "상품명";
	// 클릭된 상품의 상품명으로 replace 필요
	event["contents_path"] = "sports^상품명^공유";
	// '상품명' 부분은 클릭된 상품의 상품명으로 replace 필요
</script>
```



#### 적용예시

*NB 우먼스 클래스 6개월 패키지* 이용권의 공유 버튼을 클릭한 경우 다음과 같이 적용

**Hybrid**

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.sendClickData("EVT", "SPORTS_NB 우먼스 클래스 6개월 패키지_공유");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var event = new Object();
	event["event"] = "share";
	event["pnc"] = "asdf123";
	event["pncNm"] = "NB 우먼스 클래스 6개월 패키지";
	event["contents_path"] = "sports^NB 우먼스 클래스 6개월 패키지^공유";
	DOT.logEvent(event);
</script>
```



## 화면별 페이지뷰 측정용 API 추가

MyNB 앱 내에 있는 화면들의 페이지뷰를 측정하기 위해 대상 화면에 API를 추가해야 합니다. 아래 내용을 참고하여 API를 적용해 주시기 바랍니다.



### 매핑 테이블

API 적용 중 각 화면의 '화면코드'를 입력하는 부분이 있습니다. 이 '화면코드'는 반드시 아래 테이블에 정의된 값을 사용해 주시기 바랍니다.

| 번호 | 화면 명칭 | 화면코드 | 참고 이미지 |
| :---: | --- | --- | --- |
| 1 | 로그인 | login | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/login.jpg) |
| 2 | ID찾기 | myid | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/myid.jpg) |
| 3 | 비밀번호 찾기 | mypass | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/mypass.jpg) |
| 4 | 회원가입 유형 선택 | jointype | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/jointype.jpg) |
| 5 | 약관동의 | join01 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/join01.jpg) |
| 6 | 약관동의(영문) | join01e | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/join01e.jpg) |
| 7 | 회원정보 입력 | join02 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/join02.jpg) |
| 8 | 회원정보 입력(영문) | join02e | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/join02e.jpg) |
| 9 | 포인트 | points | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/points.jpg) |
| 10 | 퀴즈 리스트 | quizlist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/quizlist.jpg) |
| 11 | 퀴즈 상세 | quiz | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/quiz.jpg) |
| 12 | 기부 캠페인 리스트 | donlist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/donlist.jpg) |
| 13 | 기부 캠페인 상세 | donation | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/donation.jpg) |
| 14 | 나의 기부내역 | donor | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/donor.jpg) |
| 15 | 상품 쿠폰 전환 | goods | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/goods.jpg) |
| 16 | 액티비티 쿠폰전환 | actcoup | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/actcoup.jpg) |
| 17 | MyNB 출석체크 | cal01 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/cal01.jpg) |
| 18 | 친구초대 | invite | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/invite.jpg) |
| 19 | 포스트 리스트 | postlist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/postlist.jpg) |
| 20 | 포스트 상세 | post | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/post.jpg) |
| 21 | 이벤트 리스트 | evtlist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/evtlist.jpg) |
| 22 | 이벤트 상세 | event | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/event.jpg) |
| 23 | 스포츠 | sports | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/sport-00.jpg) |
| 24 | 우먼스클래스 리스트 | clslist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/classlist.jpg) |
| 25 | 우먼스클래스 이용권 리스트 | ticlist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/ticlist.jpg) |
| 26 | NBRC 리스트 | nbrclist | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/nbrclist.jpg) |
| 27 | 스트라바 연동 | connect | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/connect.jpg) |
| 28 | 스트라바 | strava | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/strava.jpg) |
| 29 | 스트라바 포인트 전환 | pointex | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/pointex.jpg) |
| 30 | 나의 러닝 | myrun | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/myrun.jpg) |
| 31 | NBRC 출석체크 | cal02 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/cal02.jpg) |
| 32 | 멤버십 등급 | levelup | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/levelup.jpg) |
| 33 | MyNB Point | mypoint | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/mypoint.jpg) |
| 34 | 마일리지 통합 | mileage0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/mileage0.jpg) |
| 35 | 마일리지 | mileage | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/mileage.jpg) |
| 36 | 마이 쿠폰 | coupon | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/coupon.jpg) |
| 37 | 쿠폰 교환하기 | coupon0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/coupon0.jpg) |
| 38 | 마이 액티비티 | activity | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/activity.jpg) |
| 39 | 사용 안내 | guide | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/guide.jpg) |
| 40 | 포인트 사용안내 | ptguide | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/ptguide.jpg) |
| 41 | 고객센터 | cs | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/cs.jpg) |
| 42 | A/S | service | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/service.jpg) |
| 43 | 공지사항 | notice | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/notice.jpg) |
| 44 | 1:1문의 | inquiry | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/inquiry.jpg) |
| 45 | FAQ | faq | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/faq.jpg) |
| 46 | 회원정보수정 | editinfo | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/editinfo.jpg) |
| 47 | 홈 | home | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/home.jpg) |
| 48 | 랭킹 | ranking | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/ranking.jpg) |
| 49 | NB Play | nbplay | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/nbplay.jpg) |
| 50 | 상품상세 | PDV | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/PDV.jpg) |
| 51 | 주문서 | ODF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/ODF.jpg) |
| 52 | 바코드 | barcode | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/barcode.jpg) |
| 53 | 설정 | setting | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/setting.jpg) |



### 상품 화면

MyNB 앱에서의 상품이란 우먼스 클래스, 우먼스 클래스 이용권, NBRC를 의미합니다(유료 결제가 가능한 것들). 우먼스 클래스, 우먼스 클래스 이용권, NBRC 상세화면 내에 아래 코드를 추가해 주세요.



#### 주의사항

상기 화면에 기 적용된 와이즈트래커 코드가 있을 것입니다. 해당 코드를 아래 내용으로 업데이트 해주시기 바랍니다.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setProduct("상품ID", "상품명");
	// '상품ID'와 '상품명'은 해당 화면에 노출된 상품의 ID와 명칭으로 replace 필요
	WiseTracker.setPageIdentity("PDV");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "view_product";
	screen["pi"] = "PDV";
	var product = new Object();
	product["pnc"] = "상품ID";
	product["pncNm"] = "상품명";
	// '상품ID'와 '상품명'은 해당 화면에 노출된 상품의 ID와 명칭으로 replace 필요
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'7월 케틀벨 워크아웃(2회)' 우먼스 클래스의 화면 내에 경우 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setProduct("zxc123", "7월 케틀벨 워크아웃(2회)");
	WiseTracker.setPageIdentity("PDV");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "view_product";
	screen["pi"] = "PDV";
	var product = new Object();
	product["pnc"] = "zxc123";
	product["pncNm"] = "7월 케틀벨 워크아웃(2회)";
	screen["product"] = product;
	DOT.logScreen(screen);
</script>
```



### 로그인 화면 - Hybrid

위 매핑 테이블에서 1번부터 3번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "login";
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'비밀번호 찾기' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("mypass");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "login";
	screen["pi"] = "mypass";
	DOT.logScreen(screen);
</script>
```



### 회원가입 화면 - Hybrid

위 매핑 테이블에서 4번부터 8번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "signup";
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'약관동의(영문) ' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("join01e");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "signup";
	screen["pi"] = "join01e";
	DOT.logScreen(screen);
</script>
```



### 포인트 화면 - Hybrid

위 매핑 테이블에서 9번부터 18번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'MyNB 출석체크 ' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("cal01");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "cal01";
	DOT.logScreen(screen);
</script>
```



### 퀴즈 상세 화면 - Hybrid

위 매핑 테이블의 11번인 '퀴즈 상세' 화면에는 아래 코드를 적용해 주세요.


#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("quiz");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "quiz";
	screen["serise_name"] = "퀴즈명";
	// '퀴즈명'부분은 실제 퀴즈의 명칭으로 replace 필요
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'16회차' 퀴즈의 상세 화면에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("quiz");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "quiz";
	screen["serise_name"] = "16회차";
	DOT.logScreen(screen);
</script>
```



### 기부 캠페인 상세 화면 - Hybrid

위 매핑 테이블의 13번인 '기부 캠페인 상세' 화면에는 아래 코드를 적용해 주세요.


#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("donation");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "donation";
	screen["campaign_name"] = "기부캠페인명";
	// '기부캠페인명' 부분은 실제 기부 캠페인의 명칭으로 replace 필요
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'러닝을 좋아하는 15살 주원이 이야기' 캠페인의 상세 화면에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("donation");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "point";
	screen["pi"] = "donation";
	screen["campaign_name"] = "러닝을 좋아하는 15살 주원이 이야기";
	DOT.logScreen(screen);
</script>
```



### 포스트 리스트 화면 - Hybrid

위 매핑 테이블의 19번 '포스트 리스트' 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("postlist");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "post";
	screen["pi"] = "postlist";
	DOT.logScreen(screen);
</script>
```



### 포스트 상세 화면 - Hybrid

위 매핑 테이블의 20번 '포스트 상세' 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("post");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "post";
	screen["pi"] = "post";
	screen["content_name"] = "포스트제목";
	// '포스트제목'부분은 실제 포스트의 제목으로 replace 필요
	DOT.logScreen(screen);
</script>
```



#### 적용예시

MS327 Review 포스트 내에 다음 코드 추가

``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("post");
</script>

<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "post";
	screen["pi"] = "post";
	screen["content_name"] = "MS327 Review";
	DOT.logScreen(screen);
</script>
```



### 이벤트 리스트 화면 - Hybrid

위 매핑 테이블의 21번 '이벤트 리스트' 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("evtlist");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "event";
	screen["pi"] = "evtlist";
	DOT.logScreen(screen);
</script>
```



### 이벤트 상세 화면 - Hybrid

위 매핑 테이블의 22번 '이벤트 상세' 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("event");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "event";
	screen["pi"] = "event";
	screen["event_name"] = "이벤트제목";
	// '이벤트제목'부분은 실제 이벤트의 제목으로 replace 필요
	DOT.logScreen(screen);
</script>
```



#### 적용예시

MEMBERS WEEK 이벤트 상세화면 내에 다음 코드 추가

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("event");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "event";
	screen["pi"] = "event";
	screen["event_name"] = "MEMBERS WEEK";
	DOT.logScreen(screen);
</script>
```



### 스포츠 화면 - Hybrid

위 매핑 테이블에서 23번부터 31번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "sports";
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'NBRC 리스트' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("nbrclist");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "sports";
	screen["pi"] = "nbrclist";
	DOT.logScreen(screen);
</script>
```



### 메뉴 화면 - Hybrid

위 매핑 테이블에서 32번부터 46번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "menu";
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'멤버십 등급' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("levelup");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["event"] = "menu";
	screen["pi"] = "levelup";
	DOT.logScreen(screen);
</script>
```



### 기타 화면 - Hybrid

위 매핑 테이블에서 47번부터 51번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	WiseTracker.setPageIdentity("화면코드");
	// '화면코드'는 반드시 매핑 테이블 참고
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
// 스크립트 타입이 일반적인 javascript가 아님을 주의
	var screen = new Object();
	screen["pi"] = "화면코드";
	// '화면코드'는 반드시 매핑 테이블 참고
	DOT.logScreen(screen);
</script>
```



#### 적용예시

'홈' 화면 내에 다음과 같이 적용

``` html
//V1
<script type="wisetracker/text" id="wiseTracker">
    WiseTracker.setPageIdentity("home");
</script>

//V2
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["pi"] = "home";
	DOT.logScreen(screen);
</script>
```



### 네이티브 화면

위 매핑 테이블에서 52번부터 53번까지에 해당하는 화면들에는, 화면 내에 아래 코드를 적용해 주세요.



#### 측정 API

**Android**

``` java
//V1
WiseTracker.setPageIdentity("화면코드");
// '화면코드'는 반드시 매핑 테이블 참고

//V2
Map<String, Object> pageMap = new HashMap<>();
pageMap.put("event", "menu");
pageMap.put("pi", "화면코드");
// '화면코드'는 반드시 매핑 테이블 참고
DOT.logScreen(pageMap);
```


**iOS - Swift**

``` swift
//V1
WiseTracker.setPageIdentity("화면코드")
// '화면코드'는 반드시 매핑 테이블 참고


//V2
let screen = NSMutableDictionary()
screen["event"] = "menu"
screen["pi"] = "화면코드"
// '화면코드'는 반드시 매핑 테이블 참고
DOT.logScreen(screen)
```



#### 적용예시

'바코드' 화면 내에 다음과 같이 적용



**Android**

``` java
//V1
WiseTracker.setPageIdentity("barcode");

//V2
Map<String, Object> pageMap = new HashMap<>();
pageMap.put("event", "menu");
pageMap.put("pi", "barcode");
// '화면코드'는 반드시 매핑 테이블 참고
DOT.logScreen(pageMap);
```


**iOS - Swift**

``` swift
//V1
WiseTracker.setPageIdentity("barcode")

//v2
let screen = NSMutableDictionary()
screen["event"] = "menu"
screen["pi"] = "barcode"
DOT.logScreen(screen)
```




## 웹 컨버전 스크립트 추가

MyNB 앱 내의 링크를 클릭해 온라인샵으로 랜딩된 후 발생하는 구매 전환을 측정하기 위해 다음 두가지 작업이 필요합니다.



### 웹 SDK 추가

온라인샵(m.nbkorea.com)에 와이즈트래커 웹 SDK를 아래와 같이 추가합니다. 사이트 전역에 include 되어야 합니다.

``` html
<head>
...
<script src="https://cdn.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>
</head>
```



그리고 사이트 모든 페이지의 `$(document).ready()` 내에서 와이즈트래커 초기화 함수를 호출해 주시기 바랍니다.

``` javascript
$(document).ready(function(){
	_wiseWebTrack.init({_wtno:10028,_wthst:"trk.wisetracker.co.kr",_wtufn:"ALL"});
	// webTracker 초기화
});
```



### 구매 측정

온라인샵의 구매 완료 화면에 아래 코드를 추가해 주세요.



**측정 API**

``` javascript
_wiseWebTrack.js2sSendToServer({
		PAGES:[{"pi":"ODR"}],
		REVENUE:[{"ea":"구매수량","amt":"구매금액","pnc":"상품ID","ordNo":"주문번호"}]
});
```



**적용예시 1**

*NB X T&T FLIPFLOP* 1개를 구매한 경우 구매 완료 화면에 다음과 같이 적용

``` javascript
_wiseWebTrack.js2sSendToServer({
		PAGES:[{"pi":"ODR"}],
		REVENUE:[{"ea":"1","amt":"44000","pnc":"NBRJAF410B","ordNo":"tr123456"}]
});
```



**적용예시 2**

*NB X T&T FLIPFLOP* 1개와 *ML850KL1* 2개를 구매한 경우 구매 완료 화면에 다음과 같이 적용

``` javascript
_wiseWebTrack.js2sSendToServer({
		PAGES:[{"pi":"ODR"}],
		REVENUE:[{"ea":"1;2","amt":"44000;278000","pnc":"NBRJAF410B;NBPDAS192Q","ordNo":"tr98765"}]
		// 세미콜론을 구분자로 사용하여 하나의 value 내에 복수의 정보를 입력하게 됨
});
```

