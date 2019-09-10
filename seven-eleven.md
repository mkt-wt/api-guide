# Wisetracker Integration Guide
'세븐일레븐'앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./seven-eleven.md#SDK-삽입)
* [분석 API](./seven-eleven.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./seven-eleven.md#Hybrid-영역-태깅-참고사항)
	* [회원 가입 분석](./seven-eleven.md#회원-가입-분석)
		* [주의사항](./seven-eleven.md#분석-코드)
		* [분석 코드](./seven-eleven.md#분석-코드)
* [적용 후 데이터 검증](./seven-eleven.md#적용-후-데이터-검증)
	* [AOS](./seven-eleven.md#AOS)
	* [iOS](./seven-eleven.md#iOS)


# SDK 삽입
각 플랫폼별 온라인 가이드를 참고해서 SDK를 삽입해 주시면 됩니다. 반드시 Facebook 관련 설정까지 앱에 추가해 주세요.

#### -[AOS](https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme)
#### -[iOS](https://github.com/WisetrackerTechteam/wisetrackerSDK)

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
세븐일레븐 앱 안에서 '회원가입' 버튼이 클릭되는 이벤트에 아래 코드를 추가합니다.

#### 주의사항
아래 그림과 같이 앱 안에 존재하는 모든 회원가입 버튼이 클릭되는 시점에 분석 코드가 읽히도록 설정해야 합니다.

#### 분석 코드
AOS
``` kotlin
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"RGR"];
[WiseTracker setGoal:@"g1" value: 1];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("RGR")
WiseTracker.setGoal("g1", 1)
WiseTracker.sendTransaction()
```

Hybrid
``` html
<!-- 회원가입 버튼 클릭 시점에 코드 삽입 -->
<script type="wisetracker/text" id="wiseTracker">
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
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
