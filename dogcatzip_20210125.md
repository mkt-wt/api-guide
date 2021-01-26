# Wisetracker Integration Guide
'개고집' 앱에서 추가 데이터를 측정하는데 필요한 코드를 적용하는 방법을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [본인인증 완료 측정](./dogcatzip_20210125.md#본인인증-완료-측정)
* [유저 정보 측정](./dogcatzip_20210125.md#유저-정보-측정)
* [반려동물 등록 측정 - 회원가입 단계에서](./dogcatzip_20210125.md#반려동물-등록-측정---회원가입-단계에서)
* [반려동물 등록 측정 - 마이 페이지에서](./dogcatzip_20210125.md#반려동물-등록-측정---마이-페이지에서)
* [이벤트 공유하기 측정](./dogcatzip_20210125.md#이벤트-공유하기-측정)
* [제품 조회 측정](./dogcatzip_20210125.md#제품-조회-측정)
* [제품 식품첨가물 전체보기 측정](./dogcatzip_20210125.md#제품-식품첨가물-전체보기-측정)
* [제품 전체원료보기 측정](./dogcatzip_20210125.md#제품-전체원료보기-측정)
* [제품 온라인 가격 보러가기 측정](./dogcatzip_20210125.md#제품-온라인-가격-보러가기-측정)
* [제품 리뷰 전체보기 측정](./dogcatzip_20210125.md#제품-리뷰-전체보기-측정)
* [제품 리뷰등록 완료 측정](./dogcatzip_20210125.md#제품-리뷰등록-완료-측정)
* [홈화면 카테고리메뉴 클릭 측정](./dogcatzip_20210125.md#홈화면-카테고리메뉴-클릭-측정)
* [맞춤검색화면 조회 측정](./dogcatzip_20210125.md#맞춤검색화면-조회-측정)
* [카테고리검색화면 조회 측정](./dogcatzip_20210125.md#카테고리검색화면-조회-측정)
* [검색 완료 측정](./dogcatzip_20210125.md#검색-완료-측정)
* [적용 후 검증](./dogcatzip_20210120.md#적용-후-검증)



## 본인인증 완료 측정

앱 내에서 본인인증이 완료된 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 본인인증이 완료되는 시점에 적용해 주시기 바랍니다. 총 3곳에서 본인인증이 가능한 것으로 전달 받았으며, 어디에서 인증이 완료되는지에 따라 서로 다른 값이 코드에 추가되어야 합니다.


### 매핑 테이블

아래 테이블에 있는 `authType`의 값을 분석 코드에 추가해야 합니다.

| 본인인증 위치 | authType |
|---|---|
| 회원가입 단계 | certify_signup |
| 마이 페이지 | certify_my |
| 이벤트 신청 페이지 | certify_event |


### 분석 코드

**Flutter**

```dart
var event = {};
event["event"] = "authType"; // authType 을 매핑 테이블의 코드값으로 치환
DOT.logEvent(event);
```

### 적용 예시

유저가 마이 페이지에서 본인인증을 완료한 경우, 완료 시점에 아래 코드 추가

**Flutter**

```dart
var event = {};
event["event"] = "certify_my";
DOT.logEvent(event);
```

## 유저 정보 측정

로그인 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 앱에 로그인이 완료된 시점에 적용해 주시기 바랍니다. **자동 로그인**에도 적용되어야 합니다.
* 주의사항 - 앱에서 로그인이 완료되는 시점에 '로그인 완료 측정'용 코드가 적용되어 있을 것입니다. '유저 정보 측정' 코드가 '로그인 완료 측정' 코드보다 위에 위치하도록 적용해 주시기 바랍니다.


### 매핑 테이블

아래 테이블에 있는 `ageGroup` 값을 분석 코드에 추가해야 합니다.

| 연령대 | ageGroup | 설명 |
|---|---|---|
| 10세 미만 | kids | 0 - 9세까지 |
| 10대 | teens | 10 - 19세까지 |
| 20대 | twenties | 20 - 29세까지 |
| 30대 | thirties | 30 - 39세까지 |
| 40대 | forties | 40 - 49세까지 |
| 50대 | fifties | 50 - 59세까지 |
| 60대 | sixties | 60 - 69세까지 |
| 70대 이상 | over seventies | 70세 이상 |

### 분석 코드

**Flutter**

```dart
var user = {};
user["sx"] = "회원 성별"; // male, female 2가지로 구분
user["ag"] = "회원 연령"; // 매핑 테이블에 있는 값으로 치환
user["ut5"] = "보유한 스티커 개수"; // 숫자를 string으로 입력
DOT.setUser(json.encode(user));
```

### 적용 예시

30대 여성이며 스티커가 없는 유저가 카카오 계정으로 로그인을 완료한 경우, 완료 시점에 아래 코드 추가

**Flutter**

map을 string으로 변환할때 사용하는 convert Library를 import 해주세요.

```dart
import 'dart:convert';
```

```dart
var user = {};
user["sx"] = "female";
user["ag"] = "thirties";
user["ut5"] = "0";
DOT.setUser(json.encode(user));

// 아래는 기존에 추가된 로그인 측정용 코드
// 유저 정보 측정용 코드가 로그인 측정용 코드보다 위쪽에 있어야 함
var event = {};
event["event"] = "w_login_complete";
event["loginTp"] = "kakao";
DOT.logEvent(event);
```


## 반려동물 등록 측정 - 회원가입 단계에서

이 부분은 [기존에 적용하셨던 내용](https://github.com/mkt-wt/api-guide/blob/master/dogcatzip_20210120.md#%EB%B0%98%EB%A0%A4%EB%8F%99%EB%AC%BC-%EB%93%B1%EB%A1%9D-%EC%B8%A1%EC%A0%95)을 수정하는 성격이 있습니다. 반려동물 등록이 '회원가입 단계'와 '마이페이지' 2군데에서 가능하기 때문에 이것을 구분해서 봐야 한다는 고객사의 니즈를 반영하여 수정이 필요합니다. 수정 사항을 요약하면 다음과 같습니다.

1. 수정사항 요약
	* 기존에 사용하던 key 값들 변경
	* 반려동물 연령을 1년 단위로 입력하도록 변경 (n 개월 단위는 사용하지 않음)
	* 반려동물 '관리가 필요한 부분' 과 '알러지 / 먹으면 안되는 것' 정보 추가 수집하도록 변경
	* 반려동물 등록번호는 수집하지 않고, 등록번호를 등록한 횟수를 수집하도록 변경
	* 'event' key에 세팅하던 value 변경 

2. 코드 적용 시점 - **회원가입 단계**에서 반려동물이 등록 완료된 시점에 코드를 적용해 주시기 바랍니다.



### 분석 코드

**Flutter**

```dart
var user = {};
user["ut1"] = "반려동물 연령"; // 1년 단위로 입력, 1년 미만인 경우도 1년으로 간주, 숫자를 string으로 입력
user["ut2"] = "반려동물 품종";
// 아래 라인은 별도의 설명 필요. 반드시 적용 예시를 참고해 주세요.
// 2개 이상의 항목이 선택된 경우 선택된 모든 항목을 붙여서 입력하되, vertical bar로 텍스트를 구분 
user["ut3"] = "관리가 필요한 부분";
user["ut4"] = "알러지 / 먹으면 안되는 것";
DOT.setUser(json.encode(user));

var event = {};
event["event"] = "pet_register_signup"; // 회원가입 단계에서 등록되었다는 것을 의미하게 됨
event["character_type"] = "반려동물 종";
event["character_name"] = "반려동물 성별";
event["g30"] = 1; // 등록 번호가 입력된 경우에만 이 라인을 적용함, 등록번호 없이 반려동물이 등록된 경우는 이 라인 제외
DOT.logEvent(event)
```

### 적용 예시

2개월된 중성화된 남아 진돗개이며, 관리가 필요한 부분은 '없음', 알러지 는 '소', '닭', '오리' 이고, 등록번호 없이 등록 완료한 경우, 등록 완료 시점에 아래 코드 추가

**Flutter**

map을 string으로 변환할때 사용하는 convert Library를 import 해주세요.

```dart
import 'dart:convert';
```

```dart
var user = {};
user["ut1"] = "1"; // 1년 미만인 경우도 1세로 간주
user["ut2"] = "진돗개";
user["ut3"] = "없음";
user["ut4"] = "소|닭|오리"; // 선택된 각 항목들을 모두 붙여서 입력해주되 각 텍스트를 | 로 구분함, 텍스트와 텍스트 사이에 공백이 들어가지 않도록 주의 
DOT.setUser(json.encode(user));

var event = {};
event["event"] = "pet_register_signup";
event["character_type"] = "강아지";
event["character_name"] = "남아 (중성화)";
DOT.logEvent(event);
```

3년된 여아 골든 리트리버이며, 관리가 필요한 부분은 '눈물 자국' 과 '뼈/관절', 알러지 는 '기타' 이고, 등록번호도 입력해서 등록 완료한 경우, 등록 완료 시점에 아래 코드 추가

**Flutter**

map을 string으로 변환할때 사용하는 convert Library를 import 해주세요.

```dart
import 'dart:convert';
```

```dart
var user = {};
user["ut1"] = "3";
user["ut2"] = "골든 리트리버";
user["ut3"] = "눈물 자국|뼈/관절"; // 선택된 각 항목들을 모두 붙여서 입력해주되 각 텍스트를 | 로 구분함, 텍스트와 텍스트 사이에 공백이 들어가지 않도록 주의
user["ut4"] = "기타";
DOT.setUser(json.encode(user));

var event = {};
event["event"] = "pet_register_signup";
event["character_type"] = "강아지";
event["character_name"] = "여아";
event["g30"] = 1; // 등록 번호가 있는 경우 본 라인 추가
DOT.logEvent(event);
```


## 반려동물 등록 측정 - 마이 페이지에서

이 부분은 [기존에 적용하셨던 내용](https://github.com/mkt-wt/api-guide/blob/master/dogcatzip_20210120.md#%EB%B0%98%EB%A0%A4%EB%8F%99%EB%AC%BC-%EB%93%B1%EB%A1%9D-%EC%B8%A1%EC%A0%95)을 수정하는 성격이 있습니다. 반려동물 등록이 '회원가입 단계'와 '마이페이지' 2군데에서 가능하기 때문에 이것을 구분해서 봐야 한다는 고객사의 니즈를 반영하여 수정이 필요합니다. 수정 사항을 요약하면 다음과 같습니다.

1. 수정사항 요약
	* 기존에 사용하던 key 값들 변경
	* 반려동물 연령을 1년 단위로 입력하도록 변경 (n 개월 단위는 사용하지 않음)
	* 반려동물 '관리가 필요한 부분' 과 '알러지 / 먹으면 안되는 것' 정보 추가 수집하도록 변경
	* 반려동물 등록번호는 수집하지 않고, 등록번호를 등록한 횟수를 수집하도록 변경
	* 'event' key에 세팅하던 value 변경

2. 코드 적용 시점 - **마이 페이지**에서 반려동물이 등록 완료된 시점에 코드를 적용해 주시기 바랍니다.


### 분석 코드

**Flutter**

```dart
var user = {};
user["ut1"] = "반려동물 연령"; // 1년 단위로 입력, 1년 미만인 경우도 1년으로 간주, 숫자를 string으로 입력
user["ut2"] = "반려동물 품종";
// 아래 라인은 별도의 설명 필요. 반드시 적용 예시를 참고해 주세요.
// 2개 이상의 항목이 선택된 경우 선택된 모든 항목을 붙여서 입력하되, vertical bar로 텍스트를 구분 
user["ut3"] = "관리가 필요한 부분";
user["ut4"] = "알러지 / 먹으면 안되는 것";
DOT.setUser(json.encode(user));

var event = {};
event["event"] = "pet_register_my"; // 마이 페이지에서 등록되었다는 것을 의미하게 됨
event["character_type"] = "반려동물 종";
event["character_name"] = "반려동물 성별";
event["g30"] = "1"; // 등록 번호가 입력된 경우에만 이 라인을 적용함, 등록번호 없이 반려동물이 등록된 경우는 이 라인 제외
DOT.logEvent(event)
```


## 이벤트 공유하기 측정
이벤트 상세화면에 있는 '이벤트 공유하기' 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 이벤트 공유하기 버튼이 클릭되는 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.


### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "event_share";
event["event_id"] = "이벤트 고유번호";
event["event_name"] = "이벤트 명칭";
event["page_id"] = "event detail";
DOT.logEvent(event);
```

### 적용 예시

'아미오 사료 샘플 배송비 체험' 이벤트의 '이벤트 공유하기' 버튼이 클릭된 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "event_share";
event["event_id"] = "75";  // 해당 이벤트의 고유한 key 값 입력
event["event_name"] = "아미오 사료 샘플 배송비 체험";
event["page_id"] = "event detail";
DOT.logEvent(event);
```



## 이벤트 상세화면 조회 측정

개별 이벤트 단위로 조회수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 이벤트 상세화면 내에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_event";
screen["event_id"] = "이벤트 고유번호";
screen["event_name"] = "이벤트 명칭";
screen["page_id"] = "event detail";
DOT.logScreen(screen);
```

### 적용 예시

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


## 제품 검색 측정

개별 제품 단위로 조회수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품 상세화면 내에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_product";
screen["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
screen["product"] = product;
DOT.logScreen(screen);
```

### 적용 예시

'더블미트 연어 캣' 제품의 상세 화면 내에 아래 코드 적용

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_product";
screen["page_id"] = "product detail";
var product = {};
product["product_id"] = "1779"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "더블미트 연어 캣";
product["category_name_a"] = "사료";
product["brand_name"] = "ANF";
screen["product"] = product;
DOT.logScreen(screen);
```



## 제품 조회 측정

개별 제품 단위로 조회수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품 상세화면 내에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_product";
screen["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
screen["product"] = product;
DOT.logScreen(screen);
```

### 적용 예시

'더블미트 연어 캣' 제품의 상세 화면 내에 아래 코드 적용

**Flutter**

```dart
var screen = {};
screen["event"] = "w_view_product";
screen["page_id"] = "product detail";
var product = {};
product["product_id"] = "1779"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "더블미트 연어 캣";
product["category_name_a"] = "사료";
product["brand_name"] = "ANF";
screen["product"] = product;
DOT.logScreen(screen);
```


## 제품 식품첨가물 전체보기 측정

개별 제품 단위로 식품첨가물 전체보기 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품 상세화면에서 '식품첨가물 전체보기'가 클릭된 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "food_additives";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
event["product"] = product;
DOT.logEvent(event);
```

### 적용 예시

'예스아임리얼 북어트릿' 제품의 상세 화면에서 식품첨가물 전체보기가 클릭된 경우, 해당 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "food_additives";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "1483"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "예스아임리얼 북어트릿";
product["category_name_a"] = "간식";
product["brand_name"] = "골드로니";
event["product"] = product;
DOT.logEvent(event);
```


## 제품 전체원료보기 측정

개별 제품 단위로 전체원료보기 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품 상세화면에서 '전체원료보기'가 클릭된 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "food_ingredients";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
event["product"] = product;
DOT.logEvent(event);
```

### 적용 예시

'펫 덴탈잼' 제품의 상세 화면에서 식품첨가물 전체보기가 클릭된 경우, 해당 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "food_ingredients";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "3021"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "펫 덴탈잼";
product["category_name_a"] = "치아";
product["brand_name"] = "독키호테";
event["product"] = product;
DOT.logEvent(event);
```


## 제품 온라인 가격 보러가기 측정

개별 제품 단위로 온라인 가격 보러가기 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품 상세화면에서 '온라인 가격 보러가기'가 클릭된 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "price_check";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
event["product"] = product;
DOT.logEvent(event);
```

### 적용 예시

'펫 덴탈잼' 제품의 상세 화면에서 온라인 가격 보러가기가 클릭된 경우, 해당 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "price_check";
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "3021"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "펫 덴탈잼";
product["category_name_a"] = "치아";
product["brand_name"] = "독키호테";
event["product"] = product;
DOT.logEvent(event);
```


## 제품 리뷰 전체보기 측정

개별 제품 단위로 리뷰 전체보기 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품의 리뷰 상세화면 내에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var screen = {};
screen["event"] = "w_see_review";
screen["page_id"] = "review detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
screen["product"] = product;
DOT.logScreen(screen);
```

### 적용 예시

'펫 덴탈잼' 제품의 리뷰 전체보기 화면 내에 아래 코드 적용

**Flutter**

```dart
var screen = {};
screen["event"] = "w_see_review";
screen["page_id"] = "review detail";
var product = {};
product["product_id"] = "3021"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "펫 덴탈잼";
product["category_name_a"] = "치아";
product["brand_name"] = "독키호테";
screen["product"] = product;
DOT.logScreen(screen);
```


## 제품 리뷰등록 완료 측정

개별 제품 단위로 리뷰가 등록된 횟수를 측정하기 위한 코드입니다.

* 코드 적용 시점 - 각 제품의 리뷰가 정상적으로 등록된 시점에 코드를 적용해 주시기 바랍니다.

### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "w_review_added";
event["page_id"] = "review register";
event["score"] = "별점"; // 5점 만점으로 평가된 별점을 string으로 입력
event["is_recommend"] = "추천 여부"; // y 또는 n 으로 입력
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
event["product"] = product;
DOT.logEvent(event);
```

### 적용 예시

'펫 덴탈잼' 제품에 대해서 별점 5점, 추천 '예'가 선택된 리뷰가 등록 완료된 경우, 해당 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "w_review_added";
event["page_id"] = "review register";
event["score"] = "5";
event["is_recommend"] = "y";
var product = {};
product["product_id"] = "3021"; // 해당 제품의 고유한 key 값 입력
product["product_name"] = "펫 덴탈잼";
product["category_name_a"] = "치아";
product["brand_name"] = "독키호테";
event["product"] = product;
DOT.logEvent(event);
```


## 홈화면 카테고리메뉴 클릭 측정

아래 표시된 각 버튼이 클릭되는 횟수를 측정하기 위한 코드입니다.

![이미지0](http://www.wisetracker.co.kr/wp-content/uploads/2021/01/002.png)

* 코드 적용 시점 - 각 버튼이 클릭된 시점(클릭 이벤트)에 코드를 적용해 주시기 바랍니다.

### 매핑 테이블

아래 테이블에 있는 `buttonName` 값을 분석 코드에 추가해야 합니다.

| 버튼 | buttonName |
|---|---|
| 강아지 사료 | 강아지 사료 |
| 강아지 간식 | 강아지 간식 |
| 강아지 치아 | 강아지 치아 |
| 강아지 간강/관리 | 강아지 간강/관리 |
| 강아지 배변/위생 | 강아지 배변/위생 |
| 강아지 목욕/미용 | 강아지 목욕/미용 |
| 고양이 사료 | 고양이 사료 |
| 고양이 캔/파우치 | 고양이 캔/파우치 |
| 고양이 간식/캣닢 | 고양이 간식/캣닢 |
| 고양이 건강/관리 | 고양이 건강/관리 |
| 고양이 배변/위생 | 고양이 배변/위생 |
| 고양이 목욕/미용 | 고양이 목욕/미용 |


### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "w_click_button";
event["button_name"] = "buttonName"; // buttonName 을 매핑 테이블의 코드값으로 치환
DOT.logEvent(event);
```


### 적용 예시

유저가 강아지 목욕/미용 버튼을 클릭한 경우, 해당 시점에 아래 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "w_click_button";
event["button_name"] = "강아지 목욕/미용";
DOT.logEvent(event);
```


## 맞춤검색화면 조회 측정

아래 표시된 화면이 조회되는 횟수를 측정하기 위한 코드입니다.

![이미지1](http://www.wisetracker.co.kr/wp-content/uploads/2021/01/KakaoTalk_20210126_143846619.jpg)

* 코드 적용 시점 - 맞춤검색화면 내에 코드를 적용해 주시기 바랍니다.


### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "custom_search";
DOT.logEvent(event);
```

## 카테고리검색화면 조회 측정

아래 표시된 화면이 조회되는 횟수를 측정하기 위한 코드입니다.

![이미지2](http://www.wisetracker.co.kr/wp-content/uploads/2021/01/KakaoTalk_20210126_143846444.jpg)

* 코드 적용 시점 - 카테고리검색화면 내에 코드를 적용해 주시기 바랍니다.


### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "category_search";
DOT.logEvent(event);
```

## 검색 완료 측정

검색이 완료된 횟수를 측정하기 위한 코드입니다. 코드를 적용할때 일부 예외적인 사항이 있으니 '적용 예시'를 잘 참고해 주시기 바랍니다.

* 코드 적용 시점 - 검색 완료화면 내에 코드를 적용해 주시기 바랍니다.


### 매핑 테이블

아래 테이블에 있는 `searchType` 값을 분석 코드에 추가해야 합니다.

| 검색 유형 | searchType | 설명 |
|---|---|---|
| 맞춤 검색 | 맞춤 검색 | 맞춤 검색에 있는 필터를 적용해서 검색이 완료된 경우 |
| 카테고리 검색 | 카테고리 검색 | 카테고리 검색에 있는 옵션을 선택해서 검색이 완료된 경우 |
| 키워드 검색 | 키워드 검색 | 검색창 내에 키워드를 입력해서 검색이 완료된 경우 |


### 분석코드

**Flutter**

```dart
var event = {};
event["event"] = "w_search";
event["search_term"] = "검색된 키워드";
event["search_type"] = "searchType";
event["g20"] = 출력된 아이템 개수; // intiger
DOT.logEvent(event);
```


### 적용 예시

맞춤 검색으로 검색을 완료하여 1000개 아이템이 리스팅된 경우, 화면 내에 아래와 같이 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "w_search";
event["search_term"] = ""; // 키워드가 없으므로 value를 세팅하지 않음, 공백문자가 들어가지 않도록 주의
event["search_type"] = "맞춤 검색";
event["g20"] = 1000;
DOT.logEvent(event);
```

카테고리 검색으로 검색을 완료하여 1000개 아이템이 리스팅된 경우, 화면 내에 아래와 같이 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "w_search";
event["search_term"] = ""; // 키워드가 없으므로 value를 세팅하지 않음, 공백문자가 들어가지 않도록 주의
event["search_type"] = "카테고리 검색";
event["g20"] = 1000;
DOT.logEvent(event);
```

검색창에 '치킨'을 입력하고 검색을 완료하여 200개 아이템이 리스팅된 경우, 화면 내에 아래와 같이 코드 적용

**Flutter**

```dart
var event = {};
event["event"] = "w_search";
event["search_term"] = "치킨";
event["search_type"] = "키워드 검색";
event["g20"] = 200;
DOT.logEvent(event);
```

## 적용 후 검증

상기 내용을 적용한 테스트앱을 아래 내용을 참고하여 저희쪽으로 보내주시기 바랍니다. 앱이 배포되기 이전에 저희가 확인을 해보고 문제가 없는 상태에서 배포될 수 있도록 도와드리기 위해 본 과정을 진행하고 있습니다.

1. APK 파일은 wisetracker@naver.com 으로 보내주시기 바랍니다.
2. iOS 앱은 fornew21c@wisetracker.co.kr, humblejohn@wisetracker.co.kr 계정을 테스트플라이트로 초대하여 공유해 주시기 바랍니다.
3. APK와 테스트플라이트 초대를 해주셨다면, 이렇게 앱을 공유해 주셨다는 것을 저희 담당자에게 메일로 안내해 주시기 바랍니다.
4. 안내해주실때 앱의 메인 액티비티를 호출하는 커스텀 스키마 정보를 함께 알려주시기 바랍니다. (AOS, iOS 모두)

