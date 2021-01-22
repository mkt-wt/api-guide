# Wisetracker Integration Guide
와이즈트래커를 '개고집' 앱에 연동하기 위한 내용을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [SDK 추가](./dogcatzip_20210120.md#SDK-추가)
* [회원가입 측정](./dogcatzip_20210120.md#회원가입-측정)
* [로그인 측정](./dogcatzip_20210120.md#로그인-측정)
* [반려동물 등록 측정](./dogcatzip_20210120.md#반려동물-등록-측정)
* [강아지/고양이 필터 클릭 측정](./dogcatzip_20210120.md#강아지고양이-필터-클릭-측정)
* [이벤트 상세화면 조회 측정](./dogcatzip_20210120.md#이벤트-상세화면-조회-측정)
* [이벤트 신청 완료 측정](./dogcatzip_20210120.md#이벤트-신청-완료-측정)
* [적용 후 검증](./dogcatzip_20210120.md#적용-후-검증)



## SDK 추가

**중요사항 1**

링크 내용 중 가장 마지막에 있는 *Facebook 광고 성과 측정* 을 제외한 나머지 모든 항목들은 필수 설정이니 꼭 적용해 주시기 바랍니다. 만약 Facebook 유료 광고를 집행하실 계획이시라면 맨 마지막에 있는 *Facebook 광고 성과 측정* 도 적용해 주셔야 합니다.

**중요사항 2**

SDK 적용 중에 *AuthorizationKey를 등록* 하는 설정이 있습니다. 개고집 앱은 10305 를 key로 등록해 주시면 됩니다. (AOS/iOS 공통)

* [Flutter SDK 플러그인 설치 가이드](http://document.wisetracker.co.kr/v2/docs/sdk/flutter/flutter-install-guide)


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

**Flutter**

```dart
var event = {};
event["event"] = "w_signup_complete";
event["signupTp"] = "signupType";
DOT.logEvent(event);
```

### 적용 예시

유저가 네이버 계정으로 회원가입을 완료한 경우, 완료 시점에 아래 코드 추가

**Flutter**

```dart
var event = {};
event["event"] = "w_signup_complete";
event["signupTp"] = "naver";
DOT.logEvent(event);
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

**Flutter**

```dart
var event = {};
event["event"] = "w_login_complete";
event["loginTp"] = "loginType";
DOT.logEvent(event);
```

### 적용 예시

유저가 카카오 계정으로 로그인을 완료한 경우, 완료 시점에 아래 코드 추가

**Flutter**

```dart
var event = {};
event["event"] = "w_login_complete";
event["loginTp"] = "kakao";
DOT.logEvent(event);
```


## 반려동물 등록 측정

유저가 앱에서 반려동물을 등록한 횟수, 그리고 등록된 반려동물 정보를 측정하기 위한 코드입니다

* 코드 적용 시점 - 반려동물이 등록 완료된 시점에 코드를 적용해 주시기 바랍니다.




### 분석 코드

**Flutter**

```dart
var user = {};
user["sx"] = "반려동물 성별";
user["ag"] = "반려동물 연령";
user["ut1"] = "반려동물 종";
user["ut2"] = "반려동물 품종";
user["ut3"] = "반려동물 등록번호";
DOT.setUser(user);

var event = {};
event["event"] = "w_create_character";
event["character_type"] = "반려동물 종";
event["character_name"] = "반려동물 품종";
DOT.logEvent(event)
```

#### 적용 예시

2개월된 중성화된 남아 진돗개를 등록번호 없이 등록 완료한 경우, 등록 완료 시점에 아래 코드 추가

**Flutter**

map을 string으로 변환할때 사용하는 convert Library를 import 해주세요.

```dart
import 'dart:convert';
```

```dart
var user = {};
user["sx"] = "남아 (중성화)";
user["ag"] = "2개월";
user["ut1"] = "강아지";
user["ut2"] = "진돗개";
user["ut3"] = ""; // 공백문자가 들어가지 않도록 주의
DOT.setUser(json.encode(user));

var event = {};
event["event"] = "w_create_character";
event["character_type"] = "강아지";
event["character_name"] = "진돗개";
DOT.logEvent(event);
```


## 강아지/고양이 필터 클릭 측정

앱 상단에 있는 강아지/고양이 필터 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 버튼이 클릭되는 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.



#### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "w_click_button";
event["button_name"] = "버튼 명칭";
// 강아지 버튼이 클릭되면 dog, 고양이 버튼이 클릭되면 cat으로 위의 '버튼 명칭'을 치환
DOT.logEvent(event);
```

#### 적용 예시

유저가 고양이 버튼을 클릭한 경우, 클릭 시점에 아래 코드 추가

**Flutter**

```dart
var event = {};
event["event"] = "w_click_button";
event["button_name"] = "cat";
DOT.logEvent(event);
```


## 이벤트 상세화면 조회 측정

개별 이벤트 단위로 조회수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 이벤트 상세화면 내에 코드를 적용해 주시기 바랍니다.

#### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_event";
screen["event_id"] = "이벤트 고유번호";
screen["event_name"] = "이벤트 명칭";
screen["page_id"] = "event detail";
DOT.logScreen(screen);
```

#### 적용 예시

'아미오 사료 샘플 배송비 체험' 이벤트 상세 화면 내에 아래 코드 적용

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_event";
screen["event_id"] = "75"; // 해당 이벤트의 고유한 key 값 입력
screen["event_name"] = "아미오 사료 샘플 배송비 체험";
screen["page_id"] = "event detail";
DOT.logScreen(screen);
```

## 이벤트 신청 완료 측정
이벤트 상세화면에 있는 '이벤트 신청' 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 이벤트 신청 버튼이 클릭되는 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.


#### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_event_participated";
screen["event_id"] = "75"; // 해당 이벤트의 고유한 key 값 입력
screen["event_name"] = "이벤트 명칭";
screen["page_id"] = "event detail";
DOT.logEvent(event);
```

#### 적용 예시

'아미오 사료 샘플 배송비 체험' 이벤트의 '이벤트 신청' 버튼이 클릭된 시점에 아래 코드 적용

**Flutter**

```dart
var screen = {};
screen["event"] = "w_event_participated";
screen["event_id"] = "이벤트 고유번호";
screen["event_name"] = "아미오 사료 샘플 배송비 체험";
screen["page_id"] = "event detail";
DOT.logEvent(event);
```

## 적용 후 검증

상기 내용을 적용한 테스트앱을 아래 내용을 참고하여 저희쪽으로 보내주시기 바랍니다. 앱이 배포되기 이전에 저희가 확인을 해보고 문제가 없는 상태에서 배포될 수 있도록 도와드리기 위해 본 과정을 진행하고 있습니다.

1. APK 파일은 wisetracker@naver.com 으로 보내주시기 바랍니다.
2. iOS 앱은 fornew21c@wisetracker.co.kr, humblejohn@wisetracker.co.kr 계정을 테스트플라이트로 초대하여 공유해 주시기 바랍니다.
3. APK와 테스트플라이트 초대를 해주셨다면, 이렇게 앱을 공유해 주셨다는 것을 저희 담당자에게 메일로 안내해 주시기 바랍니다.
4. 안내해주실때 앱의 메인 액티비티를 호출하는 커스텀 스키마 정보를 함께 알려주시기 바랍니다. (AOS, iOS 모두)

