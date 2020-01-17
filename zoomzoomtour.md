# Wisetracker Integration Guide
'줌줌투어'앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./zoomzoomtour.md#SDK-삽입)
* [분석 API](./zoomzoomtour.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./zoomzoomtour.md#Hybrid-영역-태깅-참고사항)
	* [회원 가입 분석](./zoomzoomtour.md#회원-가입-분석)
		* [주의사항](./zoomzoomtour.md#주의사항)
		* [분석 코드 - 이메일 가입](./zoomzoomtour.md#분석-코드---이메일-가입)
		* [분석 코드 - 페이스북 가입](./zoomzoomtour.md#분석-코드---페이스북-가입)
		* [분석 코드 - 네이버 가입](./zoomzoomtour.md#분석-코드---네이버-가입)
	* [위시 리스트 등록](./zoomzoomtour.md#위시-리스트-등록)
		* [주의사항](./zoomzoomtour.md#주의사항-1)
		* [분석 코드](./zoomzoomtour.md#분석-코드)
	* [문의](./zoomzoomtour.md#문의)
		* [분석 코드](./zoomzoomtour.md#분석-코드-1)
	* [예약](./zoomzoomtour.md#예약)
		* [분석 코드](./zoomzoomtour.md#분석-코드-2)
	* [결제 시작](./zoomzoomtour.md#결제-시작)
		* [분석 코드](./zoomzoomtour.md#분석-코드-3)
	* [후기 등록](./zoomzoomtour.md#후기-등록)
		* [분석 코드](./zoomzoomtour.md#분석-코드-4)
	* [결제 & 매출 분석](./zoomzoomtour.md#결제--매출-분석)
		* [주의사항](./zoomzoomtour.md#주의사항-2)
		* [분석 코드](./zoomzoomtour.md#분석-코드-5)
		* [분석 코드 적용 예시](./zoomzoomtour.md#분석-코드-적용-예시)
* [적용 후 데이터 검증](./zoomzoomtour.md#적용-후-데이터-검증)
	* [AOS](./zoomzoomtour.md#AOS)
	* [iOS](./zoomzoomtour.md#iOS)


# SDK 삽입
줌줌투어의 경우 저희 담당 개발자들과 개별적으로 SDK 연동을 진행 중이신 관계로 본 문서에서는 SDK 관련 내용을 다루지 않습니다.

## 분석 API
데이터 분석용 API와 태깅 방법을 안내합니다.

### Hybrid 영역 태깅 참고사항
Hybrid 영역에 태깅한 분석 API가 Native에 있는 SDK를 참조할 수 있도록 script의 `type`과 `id`를 설정합니다.
``` html
<!-- to Wisetracker SDK -->
<script type="wisetracker/text" id="wiseTracker">
	// APIs
</script>
```

### 회원 가입 분석
줌줌투어에는 총 세 가지 회원가입(이메일, 페이스북, 네이버)이 존재합니다. 각 가입수단을 통해 회원가입이 완료되는 시점(완료 페이지, 완료 이벤트, 완료 처리 등)에 아래 분석 코드를 설정합니다.

#### 주의사항
일반적인 회원가입 경로 외에도 페이스북으로 로그인, 네이버로 로그인 버튼을 통해서 회원 가입이 이루어지는 경우에도 분석 코드를 태깅해야 합니다.

#### 분석 코드 - 이메일 가입
``` html
<!-- 이메일 가입이 완료되는 시점에 코드 삽입 -->
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.setGoal("g6", 1);
WiseTracker.sendTransaction();
</script>
```

#### 분석 코드 - 페이스북 가입
``` html
<!-- 페이스북 가입이 완료되는 시점에 코드 삽입 -->
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.setGoal("g7", 1);
WiseTracker.sendTransaction();
</script>
```

#### 분석 코드 - 네이버 가입
``` html
<!-- 네이버 가입이 완료되는 시점에 코드 삽입 -->
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.setGoal("g8", 1);
WiseTracker.sendTransaction();
</script>
```

### 위시 리스트 등록
여행 상품에 있는 하트 버튼을 클릭하여 상품이 위시 리스트에 등록되는 이벤트에 분석 코드를 삽입합니다.
#### 주의사항
1. 상품 리스트 화면에서 하트 버튼을 클릭, 상품 상세 화면에서 하트 버튼을 클릭 두 가지 경우에 모두 코드가 들어가야 합니다.

![위시 리스트 버튼](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/001.jpg)

2. 하트 버튼을 클릭해서 위시 리스트에 등록한 다음, 다시 하트 버튼을 클릭해서 위시 리스트에서 제거 하는 경우에는 분석 코드를 설정하지 않아야 합니다. 다시 말해, 버튼 클릭을 통해 위시 리스트에 등록되는 경우에만 분석 코드를 설정하면 됩니다.


#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setGoal("g9", 1);
WiseTracker.sendGoalData();
</script>
```

### 문의
각 여행 상품의 '1:1 여행문의'로 들어간 다음에 존재하는 '문의하기' 버튼이 클릭되는 이벤트에 분석 코드를 삽입합니다.

![문의하기 버튼](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/002.jpg)

#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setGoal("g10", 1);
WiseTracker.sendGoalData();
</script>
```

### 예약
각 여행 상품에 있는 '바로 예약하기' 버튼이 클릭되는 이벤트에 분석 코드를 삽입합니다.

![예약하기 버튼](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/003.jpg)

#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setGoal("g11", 1);
WiseTracker.sendGoalData();
</script>
```

### 결제 시작
각 여행 상품에서 '바로 예약하기'를 눌렀을때 나타나는 화면에 있는 '결제하기' 버튼이 클릭되는 이벤트에 분석 코드를 삽입합니다.

![결제하기 버튼](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/004.jpg)

#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setGoal("g12", 1);
WiseTracker.sendGoalData();
</script>
```

### 후기 등록
작성한 여행 후기를 제출하는 버튼이 클릭되는 이벤트에 분석 코드를 삽입합니다.

#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setGoal("g13", 1);
WiseTracker.sendGoalData();
</script>
```

### 결제 & 매출 분석
결제 금액, 횟수, 쿠폰 & 마일리지 사용 관련한 데이터 분석을 위해 결제 완료 페이지에 분석 코드를 삽입합니다.

#### 주의사항
1. 모든 금액(결제금액, 쿠폰금액, 마일리지)은 호주달러(AUD) 기준으로 입력해야 합니다.
2. 모든 금액(결제금액, 쿠폰금액, 마일리지)은 소수점 이하 두 자리 까지 입력 가능합니다.

#### 분석 코드
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setOrderQuantityArray([상품수량]);
WiseTracker.setOrderAmountArray([결제금액]); // 사용자가 실제 결제한 금액, 호주달러 기준
WiseTracker.setOrderConversionDataArray("g3", [쿠폰금액]); // 쿠폰 사용 금액, 호주달러 기준, 0 또는 positive value 입력
WiseTracker.setOrderConversionDataArray("g4", [마일리지]); // 마일리지 사용 금액, 호주달러 기준, 0 또는 positive value 입력
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
</script>
```

#### 분석 코드 적용 예시
사용자가 100.5 AUD짜리 여행 상품에 쿠폰할인 5.5 AUD를 적용하여 95 AUD를 결제하는 경우
``` html
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setOrderQuantityArray([1]);
WiseTracker.setOrderAmountArray([95]);
WiseTracker.setOrderConversionDataArray("g3", [5.5]);
WiseTracker.setOrderConversionDataArray("g4", [0]);
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
</script>
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

![iOS Debug Mobe](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
