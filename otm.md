# Wisetracker Integration Guide
'올레티비 모바일'앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./otm.md#SDK-삽입)
	* [AOS](./otm.md#-AOS)
	* [iOS](./otm.md#-iOS)
* [분석 API](./otm.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./otm.md#Hybrid-영역-태깅-참고사항)
	* [로그인 분석](./otm.md#로그인-분석)
		* [주의사항](./otm.md#주의사항)
		* [분석 코드 - AOS](./otm.md#분석-코드---AOS)
		* [분석 코드 - iOS Objective-C](./otm.md#분석-코드---iOS-Objective-C)
		* [분석 코드 - iOS Swift](./otm.md#분석-코드---iOS-Swift)
		* [분석 코드 - Hybrid](./otm.md#분석-코드---Hybrid)
	* [화면별 페이지뷰 분석](./otm.md#화면별-페이지뷰-분석)
		* [분석 코드 - AOS](./otm.md#분석-코드---AOS-1)
		* [분석 코드 - iOS Objective-C](./otm.md#분석-코드---iOS-Objective-C-1)
		* [분석 코드 - iOS Swift](./otm.md#분석-코드---iOS-Swift-1)
		* [분석 코드 - Hybrid](./otm.md#분석-코드---Hybrid-1)
* [적용 후 데이터 검증](./otm.md#적용-후-데이터-검증)
	* [AOS](./otm.md#AOS)
	* [iOS](./otm.md#iOS)


# SDK 삽입
아래 가이드에서 '필수연동 API' 부분 까지 설정해 주시면 됩니다. iOS 가이드의 '필수연동 API'에서는 **'주문/매출 분석'을 제외**하고 적용해 주시기 바랍니다. 그 외에 'Facebook 광고성과 분석' 설정은 OTM 앱에 Facebook SDK가 포함되어 있는 경우에 진행해 주시기 바랍니다.
#### -[AOS](https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme)
#### -[iOS](https://cocoapods.org/pods/WiseTracker)

## 분석 API
데이터 분석용 API와 태깅 방법을 안내합니다.

### Hybrid 영역 태깅 참고사항
분석 대상 화면이 웹뷰로 호출된 HTML 페이지라면, Hybrid 영역에 태깅한 분석 API가 Native에 있는 SDK를 참조할 수 있도록 script의 `type`과 `id`를 설정해야 합니다.
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

### 화면별 페이지뷰 분석
화면별 페이지뷰를 분석하기 위해서는 화면 식별용 API가 각 화면마다 태깅 되어야 합니다. 그리고 API에 각 화면에 대한 `화면코드`값을 입력해야 합니다. 화면정의 V0.9.3을 기준으로 아래 화면들에 대해 매핑된 `화면코드`를 사용해 주시기 바랍니다.

화면이름 | 화면코드
-------- | --------
로그인 | LIF
회원가입 | RGF
월정액상품 | SUBS
VOD 결제하기 | ODF
실시간TV | LIVE
메인추천 모듈 | HOMEMAIN
인기콘텐츠 | POPULAR
상품기반 무료 (나의 무료, 카테고리 무료) | FREE
매거진 | MGZ
5G특별관 (5G 프리미엄) | FIVEG
오리지널 콘텐츠 | ORIGINAL
리뷰의 신 | REVIEW
음악채널(OST) | OST
카테고리 Tab | CTGMAIN
전체 카테고리 | ALLCTG
검색결과 | SCH
콘텐츠 리스트(Scene 검색) | SCENESCH
안면인식 감정 추론 기반 추천 콘텐츠 | EMOSCH
마이페이지 | MYPAGE
캐시 | CASH
TV쿠폰 | TVCOUP
콘텐츠 이용권 | VOUCHER
무료체험권 | TRIAL
마이스타일 리포트 | MYSTYLE
구매내역(구매목록) | PAYLIST
내가 찜한 콘텐츠 | WISHLIST
좋아요 | LIKE
다운로드 | DOWNLOAD
시청내역 | WATCH
성인 19+ | RATED
올레TV 목록 | TVLIST
이벤트 | EVENT
공지 | NOTICE
인물 상세정보 | FIGURE
단편/시리즈/클립 | PDV
패키지 메인 콘텐츠 | PACKAGE

#### 분석 코드 - AOS
**[예시]** 사용자가 컨텐츠 상세화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` java
WiseTracker.setPageIdentity("PDV");
```

#### 분석 코드 - iOS Objective-C
**[예시]** 사용자가 회원가입에 필요한 정보를 입력하는 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` objc
[WiseTracker setPageIdentity:@"RGF"];
```

#### 분석 코드 - iOS Swift
**[예시]** 사용자가 마이 페이지 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` swift
WiseTracker.setPageIdentity("MYPAGE")
// 마이 페이지 화면에 대해 커스텀 정의한 화면코드인 MYPAGE를 value로 입력함
```

#### 분석 코드 - Hybrid
**[예시]** 사용자가 홈 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("HOME");
	// 홈 화면에 대해 커스텀 정의한 화면코드인 HOME을 value로 입력함
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
