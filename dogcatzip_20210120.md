# Wisetracker Integration Guide
와이즈트래커를 '개고집' 앱에 연동하기 위한 내용을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [SDK 추가](./dogcatzip_20210120.md#SDK-추가)
* [회원가입 측정](./dogcatzip_20210120.md#회원가입-측정)
* [로그인 측정](./dogcatzip_20210120.md#로그인-측정)
* [반려동물 등록 측정](./dogcatzip_20210120.md#반려동물-등록-측정)
* [강아지/고양이 필터 클릭 측정](./dogcatzip_20210120.md#강아지/고양이-필터-클릭-측정)
* [이벤트 상세화면 조회 측정](./dogcatzip_20210120.md#이벤트-상세화면-조회-측정)
* [이벤트 신청 완료 측정](./dogcatzip_20210120.md#이벤트-신청-완료-측정)
* [적용 후 검증](./dogcatzip_20210120.md#적용-후-검증)



## SDK 추가

링크 내용 중 가장 마지막에 있는 *Facebook 광고 성과 측정* 을 제외한 나머지 모든 항목들은 필수 설정이니 꼭 적용해 주시기 바랍니다. 만약 Facebook 유료 광고를 집행하실 계획이시라면 맨 마지막에 있는 *Facebook 광고 성과 측정* 도 적용해 주셔야 합니다.

* [Android SDK 설치 가이드](http://document.wisetracker.co.kr/v2/docs/sdk/android/android-install-guide)
* [iOS SDK 설치 가이드](http://document.wisetracker.co.kr/v2/docs/sdk/ios/ios-install-guide)




## 회원가입 측정
회원가입 횟수와 회원가입 유형을 측정하기 위한 코드입니다.

* 코드 적용 시점 - 회원가입이 완료되는 시점에 적용해 주시기 바랍니다. 네이버, 카카오, 이메일 등 어떠한 회원가입이든 그것이 완료되는 시점에 아래 코드가 호출되어야 합니다.



### 매핑 테이블

아래 테이블에 있는 `signupType`의 값을 분석 코드에 추가해야 합니다.

| 회원가입 유형 | signupType |
|---|---|
| 네이버 | naver |
| 카카오 | kakao |
| 구글 | google |
| 애플 | apple |
| 이메일 | email |




### 분석 코드

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_signup_complete");
eventMap.put("signupTp", "signupType"); // 매핑 테이블을 참고하여 유저가 가입시 사용한 유형 입력
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_signup_complete" forKey:@"event"];
[event setValue:@"email" forKey:@"signupType"]; // 매핑 테이블을 참고하여 유저가 가입시 사용한 유형 입력
[DOT logEvent:event];
```

**iOS - Swift**

```swift
let event = NSMutableDictionary()
event["event"] = "w_signup_complete"
event["signupTp"] = "signupType" // 매핑 테이블을 참고하여 유저가 가입시 사용한 유형 입력
DOT.logEvent(event)
```



### 적용 예시

유저가 네이버 계정으로 회원가입을 완료한 경우, 완료 시점에 아래 코드 추가

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_signup_complete");
eventMap.put("signupTp", "naver");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_signup_complete" forKey:@"event"];
[event setValue:@"naver" forKey:@"signupTp"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
let event = NSMutableDictionary()
event["event"] = "w_signup_complete"
event["signupTp"] = "naver"
DOT.logEvent(event)
```



## 로그인 측정

로그인 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 앱에 로그인이 완료된 시점에 적용해 주시기 바랍니다. **자동 로그인**에도 적용되어야 합니다.



### 매핑 테이블

아래 테이블에 있는 `loginType`의 값을 분석 코드에 추가해야 합니다.

| 로그인 유형 | loginType |
|---|---|
| 네이버 | naver |
| 카카오 | kakao |
| 구글 | google |
| 애플 | apple |
| 이메일 | email |



### 분석 코드

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_login_complete");
eventMap.put("loginTp", "loginType"); // 매핑 테이블을 참고하여 유저가 로그인시 사용한 유형 입력
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_login_complete" forKey:@"event"];
[event setValue:@"loginType" forKey:@"loginTp"]; // 매핑 테이블을 참고하여 유저가 로그인시 사용한 유형 입력
[DOT logEvent:event];
```

**iOS - Swift**

```swift
let event = NSMutableDictionary() 
event["event"] = "w_login_complete"
event["loginTp"] = "loginType" // 매핑 테이블을 참고하여 유저가 로그인시 사용한 유형 입력
DOT.logEvent(event)
```



### 적용 예시

유저가 카카오 계정으로 로그인을 완료한 경우, 완료 시점에 아래 코드 추가

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_login_complete");
eventMap.put("loginTp", "kakao");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_login_complete" forKey:@"event"];
[event setValue:@"kakao" forKey:@"loginTp"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
let event = NSMutableDictionary() 
event["event"] = "w_login_complete"
event["loginTp"] = "kakao"
DOT.logEvent(event)
```



## 반려동물 등록 측정

유저가 앱에서 반려동물을 등록한 횟수, 그리고 등록된 반려동물 정보를 측정하기 위한 코드입니다

* 코드 적용 시점 - 반려동물이 등록 완료된 시점에 코드를 적용해 주시기 바랍니다.




### 분석 코드

**Android**

```java
User user = new User.Builder()
					.setGender("반려동물 성별")
					.setAge("반려동물 연령")
					.setAttr1("반려동물 종")
					.setAttr2("반려동물 품종")
					.setAttr3("반려동물 등록번호")
					.build();
DOT.setUser(user);

Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_create_character");
eventMap.put("character_type", "반려동물 종");
eventMap.put("character_name", "반려동물 품종");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
[DOT setUser:
	[User builder:^(User *user) {
		[user setGender:@"반려동물 성별"];
		[user setAge:@"반려동물 연령"];
		[user setAttribute1:@"반려동물 종"];
		[user setAttribute2:@"반려동물 품종"];
		[user setAttribute3:@"반려동물 등록번호"];
	}]
];

NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_create_character" forKey:@"event"];
[event setValue:@"반려동물 종" forKey:@"character_type"];
[event setValue:@"반려동물 품종" forKey:@"character_name"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
DOT.setUser(
	User.builder({ (builder) in
		let user = builder as! User
		user.gender = "반려동물 성별"
		user.age = "반려동물 연령"
		user.attribute1 = "반려동물 종"
		user.attribute2 = "반려동물 품종"
		user.attribute3 = "반려동물 등록번호"
	})
)

let event = NSMutableDictionary()
event["event"] = "w_create_character"
event["character_type"] = "반려동물 종"
event["character_name"] = "반려동물 품종"
DOT.logEvent(event)
```



#### 적용 예시

2개월된 중성화된 남아 진돗개를 등록번호 없이 등록 완료한 경우, 등록 완료 시점에 아래 코드 추가

**Android**

```java
User user = new User.Builder()
					.setGender("남아 (중성화)")
					.setAge("2개월")
					.setAttr1("강아지")
					.setAttr2("진돗개")
					.setAttr3("") // 공백문자가 들어가지 않도록 주의
					.build();
DOT.setUser(user);

Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_create_character");
eventMap.put("character_type", "강아지");
eventMap.put("character_name", "진돗개");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
[DOT setUser:
	[User builder:^(User *user) {
		[user setGender:@"남아 (중성화)"];
		[user setAge:@"2개월"];
		[user setAttribute1:@"강아지"];
		[user setAttribute2:@"진돗개"];
		[user setAttribute3:@""]; // 공백문자가 들어가지 않도록 주의
	}]
];

NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_create_character" forKey:@"event"];
[event setValue:@"강아지" forKey:@"character_type"];
[event setValue:@"진돗개" forKey:@"character_name"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
DOT.setUser(
	User.builder({ (builder) in
		let user = builder as! User
		user.gender = "남아 (중성화)"
		user.age = "2개월"
		user.attribute1 = "강아지"
		user.attribute2 = "진돗개"
		user.attribute3 = "" // 공백문자가 들어가지 않도록 주의
	})
)

let event = NSMutableDictionary()
event["event"] = "w_create_character"
event["character_type"] = "강아지"
event["character_name"] = "진돗개"
DOT.logEvent(event)
```



## 강아지/고양이 필터 클릭 측정

앱 상단에 있는 강아지/고양이 필터 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 버튼이 클릭되는 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.



#### 분석코드

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_click_button");
eventMap.put("button_name", "버튼 명칭");
// 강아지 버튼이 클릭되면 dog, 고양이 버튼이 클릭되면 cat으로 위의 '버튼 명칭'을 치환
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_click_button" forKey:@"event"];
[event setValue:@"버튼 명칭" forKey:@"button_name"];
// 강아지 버튼이 클릭되면 dog, 고양이 버튼이 클릭되면 cat으로 위의 '버튼 명칭'을 치환
[DOT logEvent:event];
```

**iOS - Swift**

```swift
var event = NSMutableDictionary()
event["event"] = "w_click_button"
event["button_name"] = "버튼 명칭"
// 강아지 버튼이 클릭되면 dog, 고양이 버튼이 클릭되면 cat으로 위의 '버튼 명칭'을 치환
DOT.logEvent(event)
```



#### 적용 예시

유저가 고양이 버튼을 클릭한 경우, 클릭 시점에 아래 코드 추가

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_click_button");
eventMap.put("button_name", "cat");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_click_button" forKey:@"event"];
[event setValue:@"cat" forKey:@"button_name"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
var event = NSMutableDictionary()
event["event"] = "w_click_button"
event["button_name"] = "cat"
DOT.logEvent(event)
```



## 이벤트 상세화면 조회 측정

개별 이벤트 단위로 조회수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 이벤트 상세화면 내에 코드를 적용해 주시기 바랍니다.

#### 분석코드

**Hybrid**

```java
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_event";
	screen["event_id"] = "이벤트 고유번호";
	screen["event_name"] = "이벤트 명칭";
	screen["page_id"] = "event detail";
	DOT.logScreen(screen);
</script>
```

**Android**

```java
Map<String, Object> pageMap = new HashMap<>();
pageMap.put("event", "w_view_event");
pageMap.put("event_id", "이벤트 고유번호");
pageMap.put("event_name", "이벤트 명칭");
pageMap.put("page_id", "event detail");
DOT.logScreen(pageMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *screen = [[NSMutableDictionary alloc] init];
[screen setValue:@"w_view_event" forKey:@"event"];
[screen setValue:@"이벤트 고유번호" forKey:@"event_id"];
[screen setValue:@"이벤트 명칭" forKey:@"event_name"];
[screen setValue:@"event detail" forKey:@"page_id"];
[DOT logScreen:screen];
```

**iOS - Swift**

```swift
var screen = NSMutableDictionary()
screen["event"] = "w_view_event"
screen["event_id"] = "이벤트 고유번호"
screen["event_name"] = "이벤트 명칭"
screen["page_id"] = "event detail"
DOT.logScreen(screen)
```



#### 적용 예시

'아미오 사료 샘플 배송비 체험' 이벤트 상세 화면 내에 아래 코드 적용

**Hybrid**

```java
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_view_event";
	screen["event_id"] = "75"; // 해당 이벤트의 고유한 key 값 입력
	screen["event_name"] = "아미오 사료 샘플 배송비 체험";
	screen["page_id"] = "event detail";
	DOT.logScreen(screen);
</script>
```

**Android**

```java
Map<String, Object> pageMap = new HashMap<>();
pageMap.put("event", "w_view_event");
pageMap.put("event_id", "75"); // 해당 이벤트의 고유한 key 값 입력
pageMap.put("event_name", "아미오 사료 샘플 배송비 체험");
pageMap.put("page_id", "event detail");
DOT.logScreen(pageMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *screen = [[NSMutableDictionary alloc] init];
[screen setValue:@"w_view_event" forKey:@"event"];
[screen setValue:@"75" forKey:@"event_id"]; // 해당 이벤트의 고유한 key 값 입력
[screen setValue:@"아미오 사료 샘플 배송비 체험" forKey:@"event_name"];
[screen setValue:@"event detail" forKey:@"page_id"];
[DOT logScreen:screen];
```

**iOS - Swift**

```swift
var screen = NSMutableDictionary()
screen["event"] = "w_view_event"
screen["event_id"] = "75" // 해당 이벤트의 고유한 key 값 입력
screen["event_name"] = "아미오 사료 샘플 배송비 체험"
screen["page_id"] = "event detail"
DOT.logScreen(screen)
```



## 이벤트 신청 완료 측정
이벤트 상세화면에 있는 '이벤트 신청' 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 이벤트 신청 버튼이 클릭되는 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.



#### 분석코드

**Hybrid**

```java
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_event_participated";
	screen["event_id"] = "75"; // 해당 이벤트의 고유한 key 값 입력
	screen["event_name"] = "이벤트 명칭";
	screen["page_id"] = "event detail";
	DOT.logEvent(event);
</script>
```

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_event_participated");
eventMap.put("event_id", "75"); // 해당 이벤트의 고유한 key 값 입력
eventMap.put("event_name", "이벤트 명칭");
eventMap.put("page_id", "event detail");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_event_participated" forKey:@"event"];
[event setValue:@"75" forKey:@"event_id"]; // 해당 이벤트의 고유한 key 값 입력
[event setValue:@"이벤트 명칭" forKey:@"event_name"];
[event setValue:@"event detail" forKey:@"page_id"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
var event = NSMutableDictionary()
event["event"] = "w_event_participated"
event["event_id"] = "75" // 해당 이벤트의 고유한 key 값 입력
event["event_name"] = "이벤트 명칭"
event["page_id"] = "event detail"
DOT.logEvent(event)
```



#### 적용 예시

'아미오 사료 샘플 배송비 체험' 이벤트의 '이벤트 신청' 버튼이 클릭된 시점에 아래 코드 적용

**Hybrid**

```java
<script type="wisetracker/text" id="wiseTracker2">
	var screen = new Object();
	screen["event"] = "w_event_participated";
	screen["event_id"] = "이벤트 고유번호";
	screen["event_name"] = "아미오 사료 샘플 배송비 체험";
	screen["page_id"] = "event detail";
	DOT.logEvent(event);
</script>
```

**Android**

```java
Map<String, Object> eventMap = new HashMap<>();
eventMap.put("event", "w_event_participated");
eventMap.put("event_id", "이벤트 고유번호");
eventMap.put("event_name", "아미오 사료 샘플 배송비 체험");
eventMap.put("page_id", "event detail");
DOT.logEvent(eventMap);
```

**iOS - Objective-C**

```objectivec
NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
[event setValue:@"w_event_participated" forKey:@"event"];
[event setValue:@"이벤트 고유번호" forKey:@"event_id"];
[event setValue:@"아미오 사료 샘플 배송비 체험" forKey:@"event_name"];
[event setValue:@"event detail" forKey:@"page_id"];
[DOT logEvent:event];
```

**iOS - Swift**

```swift
var event = NSMutableDictionary()
event["event"] = "w_event_participated"
event["event_id"] = "이벤트 고유번호"
event["event_name"] = "아미오 사료 샘플 배송비 체험"
event["page_id"] = "event detail"
DOT.logEvent(event)
```



## 적용 후 검증

상기 내용을 적용한 테스트앱을 아래 내용을 참고하여 저희쪽으로 보내주시기 바랍니다.

1. 앱의 메인 액티비티를 호출하는 커스텀 스키마 정보를 함께 알려주시기 바랍니다.
2. APK 파일을 wisetracker@naver.com 으로 보내주세요.
3. APK 파일을 네이버 메일로 전송한 것에 대해서 배승민 과장(smbae@wisetracker.co.kr)에게 메일로 알려주시면 됩니다.

