서비스 언어 설정 기능 추가에 따른 태깅 가이드입니다.

# Android
### 1. SDK 버전 업데이트    
build.gradle에 있는 Wisetracker SDK 버전을 아래 버전으로 변경
```
kr.co.wisetracker.insight:SDK_V1:21.3.54
```

### 2. AndroidMenifest.xml에 아래 태그 추가
```xml
<meta-data android:name="WiseTrackerUseBaseProvider" android:value="false"></meta-data>
```

### 3. 최초 앱 실행 시 Wisetracker.init 전에 putInitData API를 사용해 서비스 언어 설정
```java
WiseTracker.putInitData(StaticValues.PARAM_SRVC_LANG, "ServiceLanguage");
WiseTracker.init();
```
**putInitData는 반드시 init 전에 호출이 되어야 합니다.**    
**서비스 언어별 설치 분석을 위한 설정**이며 한번 서비스 언어 설정을 하면 저희 SDK가 관련 값을 저장하고 있기 때문에    
매번 init 때마다 서비스 언어 설정이 바뀌지 않았는데도 관련 API를 호출하실 필요는 없습니다.

### 4. 서비스 언어 변경 시점에 서비스 언어 변경 API와 새로운 새션 발급 API 호출
```java
WiseTracker.setServiceLanguage("ServiceLanguage");
WiseTracker.createNewSession();
```
