# Wisetracker Integration Guide
'오토오아시스' 앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 업데이트 (AOS & iOS)](./auto_oasis.md#SDK-업데이트)
* [클릭 분석 API](./auto_oasis.md#클릭-분석-API)
	* [수입유 특가](./auto_oasis.md#수입유-특가)
	* [출장 정비](./auto_oasis.md#출장-정비)
	* [오토케어 워시](./auto_oasis.md#오토케어-워시)
	* [Kixx 엔진오일](./auto_oasis.md#Kixx-엔진오일)
* [화면 조회 분석 API](./auto_oasis.md#화면-조회-분석-API)
	* [메인](./auto_oasis.md#메인)
	* [설정](./auto_oasis.md#설정)
	* [차량정보 등록](./auto_oasis.md#차량정보-등록)
	* [차량정보 저장 완료](./auto_oasis.md#차량정보-저장-완료)
	* [회원가입 약관동의](./auto_oasis.md#회원가입-약관동의)
* [적용 후 데이터 검증](./auto_oasis.md#적용-후-데이터-검증)
	* [AOS](./auto_oasis.md#AOS)
	* [iOS](./auto_oasis.md#iOS)


## SDK 업데이트
지난 1월 13일에 최신버전의 SDK로 업데이트를 요청 드렸으나 진행되지 않은 것으로 확인됩니다. 이번에 추가되는 '버튼 클릭 분석'을 정상적으로 수행하기 위해서라도 SDK 업데이트가 필요합니다. 아래 링크한 가이드에는 '기존 SDK 제거' 방법과 '최신 버전 SDK로 업데이트' 방법이 함께 안내되어 있습니다. 가이드를 참고하여 두가지 작업을 진행해주시기 바랍니다.

> 오토오아시스 SDK 업데이트 가이드, https://github.com/mkt-wt/api-guide/blob/master/removing_old_sdk.md

## 클릭 분석 API
메인 화면에 추가된 O2O 서비스 버튼의 클릭수 측정을 위한 분석 API와 태깅 방법을 안내합니다.

### 수입유 특가
유저가 메인 화면에 있는 '수입유 특가' 버튼을 클릭하는 시점에 아래 코드를 추가합니다.
``` javascript
<script type="text/javascript">
	WiseTracker.setGoal("g3", 1);
	WiseTracker.sendGoalData();
</script>
```

### 출장 정비
유저가 메인 화면에 있는 '출장 정비' 버튼을 클릭하는 시점에 아래 코드를 추가합니다.
``` javascript
<script type="text/javascript">
	WiseTracker.setGoal("g4", 1);
	WiseTracker.sendGoalData();
</script>
```

### 오토케어 워시
유저가 메인 화면에 있는 '오토케어 워시' 버튼을 클릭하는 시점에 아래 코드를 추가합니다.
``` javascript
<script type="text/javascript">
	WiseTracker.setGoal("g5", 1);
	WiseTracker.sendGoalData();
</script>
```

### Kixx 엔진오일
유저가 메인 화면에 있는 'Kixx 엔진오일' 버튼을 클릭하는 시점에 아래 코드를 추가합니다.
``` javascript
<script type="text/javascript">
	WiseTracker.setGoal("g6", 1);
	WiseTracker.sendGoalData();
</script>
```

## 화면 조회 분석 API
앱 개편으로 인해 분석 코드가 영향을 받았습니다. 이에 따라 화면 PV를 분석하는 일부 코드들이 영향을 받았습니다. 아래 내용은 부정확한 데이터가 들어오고 있는 화면들에 대한 수정 방법 안내입니다. 내용을 숙지하시어 수정사항을 반영해 주시기 바랍니다.

### 메인
메인 화면 내에 아래 코드를 적용해 주시기 바랍니다.
``` html
<!-- html 페이지 상에서 와이즈트래커 SDK 참조 -->
<!-- script type 이 javascript 가 아닌 것을 주의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("MAIN001");
</script>
```

### 설정
설정 화면 내에 아래 코드를 적용해 주시기 바랍니다.
``` html
<!-- html 페이지 상에서 와이즈트래커 SDK 참조 -->
<!-- script type 이 javascript 가 아닌 것을 주의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("CONF");
</script>
```

### 차량정보 등록
차량정보 등록 화면에 있는 코드를 아래와 같이 수정해 주시기 바랍니다. 만약 코드가 없다면 아래 코드를 추가하면 됩니다.
``` html
<!-- html 페이지 상에서 와이즈트래커 SDK 참조 -->
<!-- script type 이 javascript 가 아닌 것을 주의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("CAR002"); //과거에 추가된 부분
	WiseTracker.sendTransaction(); //새로 추가할 라인
</script>
```

### 차량정보 저장 완료
차량정보가 정상적으로 등록되면 나타나는 alert 에 아래 코드를 적용해 주시기 바랍니다.
``` javascript
<script>
	alert('차량등록이 완료되었습니다.');
	// 와이즈트래커 분석코드 추가
	WiseTracker.setPageIdentity("CONF");
	WiseTracker.sendTransaction();
</script>
```

### 회원가입 약관동의
회원가입 약관동의 화면 내에 아래 코드를 적용해 주시기 바랍니다.
``` html
<!-- html 페이지 상에서 와이즈트래커 SDK 참조 -->
<!-- script type 이 javascript 가 아닌 것을 주의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("RGF004");
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

![iOS Debug Mode](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
