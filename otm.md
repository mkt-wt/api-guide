# Wisetracker Integration Guide
'올레티비 모바일'앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./otm.md#SDK-삽입)
	* [AOS](./otm.md#AOS)
	* [iOS](./otm.md#iOS)
* [분석 API](./otm.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./otm.md#Hybrid-영역-태깅-참고사항)
	* [로그인 분석](./otm.md#로그인-분석)
		* [주의사항](./otm.md#주의사항)
		* [분석 코드 - AOS](./otm.md#분석-코드---AOS)
		* [분석 코드 - iOS Objective-C](./otm.md#분석-코드---iOS-Objective-C)
		* [분석 코드 - iOS Swift](./otm.md#분석-코드---iOS-Swift)
		* [분석 코드 - Hybrid](./otm.md#분석-코드---Hybrid)
	* [특정 화면의 화면별 페이지뷰 분석](./otm.md#특정-화면의-화면별-페이지뷰-분석)
		* [주의사항](./otm.md#주의사항-1)
		* [분석 코드 - AOS](./otm.md#분석-코드---AOS-1)
		* [분석 코드 - iOS Objective-C](./otm.md#분석-코드---iOS-Objective-C-1)
		* [분석 코드 - iOS Swift](./otm.md#분석-코드---iOS-Swift-1)
		* [분석 코드 - Hybrid](./otm.md#분석-코드---Hybrid-1)
	* [화면별 페이지뷰 분석](./otm.md#화면별-페이지뷰-분석)
		* [주의사항](./otm.md#주의사항-2)
		* [분석 코드 - AOS](./otm.md#분석-코드---AOS-2)
		* [분석 코드 - iOS Objective-C](./otm.md#분석-코드---iOS-Objective-C-2)
		* [분석 코드 - iOS Swift](./otm.md#분석-코드---iOS-Swift-2)
		* [분석 코드 - Hybrid](./otm.md#분석-코드---Hybrid-2)
* [적용 후 데이터 검증](./otm.md#적용-후-데이터-검증)
	* [AOS](./otm.md#AOS)
	* [iOS](./otm.md#iOS)


# SDK 삽입
아래 가이드에서 '필수연동 API' 부분 까지 설정해 주시면 되는데, '필수연동 API'에서 '주문/매출 분석'을 제외하고 적용해 주시기 바랍니다. 그 외에 'Facebook 광고성과 분석' 설정은 OTM 앱에 Facebook SDK가 포함되어 있는 경우에 진행해 주시기 바랍니다.
#### [AOS](https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme)
#### [iOS](https://cocoapods.org/pods/WiseTracker)

## 분석 API
데이터 분석용 API와 태깅 방법을 안내합니다.

### Hybrid 영역 태깅 참고사항
Hybrid 영역에 태깅한 분석 API가 Native에 있는 SDK를 참조할 수 있도록 script의 `type`과 `id`를 설정합니다.
``` html
<!-- refer to Wisetracker SDK -->
<script type="wisetracker/text" id="wiseTracker">
	// APIs
</script>
```

### 로그인 분석
로그인이 완료되는 시점(완료 페이지, 완료 이벤트, 완료 처리 등)에 아래 분석 코드를 설정합니다.

#### 주의사항
페이스북으로 로그인, 네이버로 로그인, 자동 로그인 등 모든 로그인 완료에 분석 코드를 태깅해야 합니다.

#### 분석 코드 - AOS
``` java
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.sendGoalData();
```

#### 분석 코드 - iOS Objective-C
``` objc
[WiseTracker setPageIdentity:@"LIR"];
[WiseTracker setGoal:@"g2" value: 1];
[WiseTracker sendGoalData];
```

#### 분석 코드 - iOS Swift
``` swift
WiseTracker.setPageIdentity("LIR")
WiseTracker.setGoal("g2", 1)
WiseTracker.sendGoalData()
```

#### 분석 코드 - Hybrid
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("LIR");
	WiseTracker.setGoal("g2", 1);
	WiseTracker.sendGoalData();
</script>
```

### 특정 화면의 화면별 페이지뷰 분석
특정 화면이란, 해당 화면을 가리키는 화면코드가 와이즈트래커 시스템 상에 사전 정의되어 있는 화면들을 의미합니다. 상품 상세 화면, 주문 완료 화면 등 데이터 분석 상 중요한 화면들은 사전 정의되어 있습니다. 이런 화면들의  페이지뷰를 측정하기 위해, 각 화면 안에 아래 분석 코드를 설정합니다.

#### 주의사항
각 화면의 목록과 `화면코드`는 아래 표를 참고해 입력해 주시기 바랍니다.

화면 이름 | 화면코드
-------- | --------
컨텐츠 상세 | PDV
주문 완료 | ODR
로그인 완료 | LIR
장바구니 보기 | OCV

#### 분석 코드 - AOS
``` java
WiseTracker.setPageIdentity("화면코드");
// 컨텐츠 상세 화면인 경우 화면코드에 PDV를, 주문 완료 화면인 경우 화면코드에 ODR을 입력
```

#### 분석 코드 - iOS Objective-C
``` objc
[WiseTracker setPageIdentity:@"화면코드"];
// 컨텐츠 상세 화면인 경우 화면코드에 PDV를, 주문 완료 화면인 경우 화면코드에 ODR을 입력
```

#### 분석 코드 - iOS Swift
``` swift
WiseTracker.setPageIdentity("화면코드")
// 컨텐츠 상세 화면인 경우 화면코드에 PDV를, 주문 완료 화면인 경우 화면코드에 ODR을 입력
```

#### 분석 코드 - Hybrid
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("화면코드");
	// 컨텐츠 상세 화면인 경우 화면코드에 PDV를, 주문 완료 화면인 경우 화면코드에 ODR을 입력
</script>
```

### 화면별 페이지뷰 분석
사전 정의되지 않은 화면들의 페이지뷰를 측정하기 위해, 각 화면 안에 아래 분석 코드를 설정합니다.

#### 주의사항
각 화면을 식별하는 `화면코드`는 알파-뉴메릭 8자리까지 입력해야 합니다.
그리고 와이즈트래커 시스템에 사전 정의된 화면코드가 있습니다. 상품 상세 화면은 PDV, 

#### 분석 코드 - AOS
``` java
WiseTracker.setPageIdentity("화면코드");
```

#### 분석 코드 - iOS Objective-C
``` objc
[WiseTracker setPageIdentity:@"화면코드"];
```

#### 분석 코드 - iOS Swift
``` swift
WiseTracker.setPageIdentity("화면코드")
```

#### 분석 코드 - Hybrid
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("화면코드");
</script>
```

## 적용 후 데이터 검증
SDK와 API가 올바르게 적용 되었는지 확인하기 위해서는 아래 코드(디버그 모드 활성화)를 적용한 테스트 앱을 저희 쪽으로 보내주시면 됩니다. 보내주신 테스트 앱에서 데이터를 확인한 후 결과에 대해서 회신 드리고 있습니다.

### AOS
AndroidManifest.xml 파일에 아래 메타 데이터 태그를 추가합니다.
``` java
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
